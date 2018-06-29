# Python Tips Logging

Author 杜远超

## 简介
###  什么情况下需要使用Logging
当print不能满足需求时候，例如：终端一次输出太多内容，远程跑程序，长时间跑程序，工程中不同文件的输出，

Python提供了日志模块，可以将程序运行中的相关信息，如运行时间，描述信息以及错误或者异常发生的时候定位。

日志级别
| Level | 使用情形 |
| - | :-: | -: | 
| DEBUG | 详细信息，在追踪问题时候使用| 
| INFO | 正常信息 | 
| WARNING | 一些不可预见的问题发生，或者将要发生，如磁盘空间低，但不影响程序的运行 |
| ERROR | 由于严重问题，程序中的一些功能受到影响 |
| CRITICAL | 严重错误，或者程序本身不能运行 | 


## 多模块Logging

```
#myapp.py
import logging
import mylib
def main():
    logging.basicConfig(filename='myapp.log', level=logging.INFO)
    logging.info('Started')
    mylib.do_something()
    logging.info('Finished')

if __name__ == '__main__':
    main()
```

```
#mylib.py
import logging

def do_something():
    logging.info('Doing something')
```

当运行*myapp.py*可以在 *myapp.log* 中看到
```
INFO:root:Started
INFO:root:Doing something
INFO:root:Finished
```

## 推荐库
[glog](https://www.google.com/url?q=https%3A%2F%2Fpypi.python.org%2Fpypi%2Fglog&sa=D&sntz=1&usg=AFQjCNGoHjv0kUQcU1YK3wcoP57LbPUMUw)： A simple Google-style logging wrapper
```
import glog as log

log.setLevel("INFO")  # Integer levels are also allowed.
log.info("It works.")
log.warn("Something not ideal")
log.error("Something went wrong")
log.fatal("AAAAAAAAAAAAAAA!")
```
以下为输出
```
I0629 09:51:24.308165 74455 test.py:4] It works.
W0629 09:51:24.308538 74455 test.py:5] Something not ideal
E0629 09:51:24.308588 74455 test.py:6] Something went wrong
F0629 09:51:24.308635 74455 test.py:7] AAAAAAAAAAAAAAA!
```
log的信息说明：
1. The first character is the log level, followed by MMDD (month, day)
2. HH:MM:SS.microseconds
3. Process ID
4. basename_of_sourcefile.py:linenumber]
5. The body of the log message.




## 参考文件
1. Python Documents -- [Standar Library -- logging](https://docs.python.org/3/library/logging.html)
2. Python Documents -- [HowTO Logging](https://docs.python.org/3/howto/logging.html)