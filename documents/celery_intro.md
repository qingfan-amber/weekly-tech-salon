# Celery 简介

*author:杜远超*

## celery能解决什么问题
> Celery is an asynchronous task queue/job queue based on distributed message passing. It is focused on real-time operation, but supports scheduling as well.

异步任务队列，应用于分布式系统。处理long lasting (CPU job) while qucikly answering request。完成处理后，需要进一步出发动作，例如发邮件，更新数据库。执行外部API calls，依赖外部服务。在HTTP request-response 流程外的异步执行任务工具

1. [监控](http://docs.celeryproject.org/en/latest/userguide/monitoring.html#guide-monitoring)
2. 工作流
3. **Time & Rate limits**: You can control how many tasks can be executed per second/minute/hour, or how long a task can be allowed to run, and this can be set as a default, for a specific worker or individually for each task type.
4. Scheduling
5. Resource Leak Protection
6. User Components

## celery原理与功能模块简介

[图例](https://www.vinta.com.br/blog/2017/celery-overview-archtecture-and-how-it-works/)

Producer(WEB) -- Queue(BROKER) -- Consumer(WORKER) 



Broker：Queue
objects先进行序列化，之后存入到broker中。传入task之前再进行反序列化；如果传输比较复杂的模型，会有问题；老版本的celery中，使用Pickle进行序列化，Pickle存在安全性问题，新的celery使用JSON


### Worker
[链接](http://docs.celeryproject.org/en/latest/userguide/workers.html)
every worker maintains a mapping of task names to their actual functions, called the task registry.
可以开启多个worker
```
$ celery -A proj worker --loglevel=INFO --concurrency=10 -n worker1@%h
$ celery -A proj worker --loglevel=INFO --concurrency=10 -n worker2@%h
$ celery -A proj worker --loglevel=INFO --concurrency=10 -n worker3@%h
```
可以进行多种设置：Time Limits; Rate Limites; Max tasks per child; Max memory per child;
一个worker可以消耗多个queue。

### Task
[链接](http://docs.celeryproject.org/en/latest/userguide/tasks.html)
A task message is not removed from the queue until that message has been acknowledged by a worker. A worker can reserve many messages in advance and even if the worker is killed – by power failure or some other reason – the message will be redelivered to another worker.

All defined tasks are listed in a registry. The registry contains a list of task names and their task classes. You can investigate this registry yourself:

只有当定义了task的模块被import后，task才被注册。当发送task时，并不传送代码，只是将task的名字传送，之后worker根据message来找注册的task以及其对应的执行代码。

- 使用task decorators创建
- 必须与唯一name（若不指定，会有默认格式添加）

### Result Backend
Celery can keep track of the tasks current state. The state also contains the result of a successful task, or the exception and track back information of a failed task.
[对比各种result backend优劣的文章](http://docs.celeryproject.org/en/latest/userguide/tasks.html#task-result-backends)



```
# This goes in the `worker node`

from celery import Celery

app = Celery(...)

@app.task
def add(a, b):
    return a + b
```

```
# This goes in the `web node`

from tasks import add

r = add.delay(4, 5).get()
print(r)  # 9
```
`delay` places the task in the queue and returns a promise that can be used to monitor the status and get the result when it's ready. 

Calling `get` in that promise will block the execution until the result is available.

The `add` task has to store the result somewhere so it can then be accessed by the process that triggered it.







## celery best practices

- [Decreasing RAM Usage by 40% Using jemalloc with Python & Celery](https://zapier.com/engineering/celery-python-jemalloc/)
- [本文列举了非常多的Celery相关资料](https://www.fullstackpython.com/celery.html)
- Celery task [如何测试](https://www.python-celery.com/2018/05/01/unit-testing-celery-tasks/)
    - 调用task，程序等待执行（优势1:测试了Celery；优势2:Testcse与真实环境相同；不足1:需要message broker; 不足2:需要celery worker;不足3:不只是一个unit test）
    - 只测试函数(优势1:简单; 优势2:不依赖message broker; 优势3:不依赖celery worker; 优势4: 独立的unit test; 不足1:没有测试Celery; 不足2： Testcase与真实场景不同)
    - 异步调用程序
    ```
    def test_fetch_data(self):
        task = fetch_data.s(url='...').apply()
        self.assertEqual(task.result, 'SUCCESS')
        ...
    ```
- Celery 如何部署：[Django in Production Background Tasks](http://www.robgolding.com/blog/2011/11/27/django-in-production-part-2---background-tasks/)
    - Gunicorn (python)
    - Supervisor (python)
    - Supervisor + celeryd + worker + RabbitMQ + Monitoring
- [Full Stack Python](https://www.fullstackpython.com/table-of-contents.html)


- 关于Task的best practice
    - 如果不关心task结果，可以设置ignore
    ```
    @app.task(ignore_result=True)
    def mytask():
        something()
    ```
    - task之间不要进行嵌套

## 延展
- Pickle安全性问题
    - Python的文档清晰表明了它不提供安全性保证，因此对于一个从不可信的数据源接受的数据不要轻易进行反序列化。由于load()可以接收字符串作为参数，pickle.load("dos\nsystem\n(S'dir'\ntR.)")便可以查看当前目录下的所有文件
- celery beat 和celery worker的区别
- 为什么不用数据库作为Broker（task queue）
    - 频繁操作数据库，进行 lock引发rack conditions 
    - https://www.fullstackpython.com/celery.html
    - Asynchronous Processing in Web Applications Part One and Part Two are great reads for understanding the difference between a task queue and why you shouldn't use your database as one.
- 多语言支持
    - [celery php](https://github.com/gjedeer/celery-php)
    - [celery node](https://github.com/mher/node-celery)

### Producer-Consumer Problem
也叫Buounded-buffer Problem，是多线程同步的经典问题。这个问题中包含两类线程：生产者和消费者，他们共享一个固定大小的缓存区作为一个队列。生产者的工作是生成数据，将其放入缓存区，之后再次开始。消费者的工作是消耗数据，即将数据从缓存区中移除（每次一条）。问题在于：当缓存区满后，生产者不再向其中放入数据，当缓存区空的时候，消费者不再从其中移除数据。

解决方案是：当缓存区满后，生产者进行sleep或者抛弃数据，下次消费者移除数据后，通知生产者再次向缓存区中放数据；同样，当缓存区空了后，消费者进入sleep，等生产者在放入数据后，通知消费者再从缓存中移除数据。一个差的解决方案回到这死锁(deadlock)，两个进程都等待被唤醒。

死锁示例：
```
int itemCount = 0;

procedure producer() 
{
    while (true) 
    {
        item = produceItem();

        if (itemCount == BUFFER_SIZE) 
        {
            sleep();
        }

        putItemIntoBuffer(item);
        itemCount = itemCount + 1;

        if (itemCount == 1) 
        {
            wakeup(consumer);
        }
    }
}

procedure consumer() 
{
    while (true) 
    {

        if (itemCount == 0) 
        {
            sleep();
        }

        item = removeItemFromBuffer();
        itemCount = itemCount - 1;

        if (itemCount == BUFFER_SIZE - 1) 
        {
            wakeup(producer);
        }

        consumeItem(item);
    }
}

```

Producer -- Queue -- Consumer 





