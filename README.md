# QF_Amber团队_每周技术沙龙


Amber团队每周技术沙龙技术内容文档。
## 沙龙说明
1. 技术沙龙每周五(可调节)一次，每次由一个小组负责轮值
2. 轮值顺序为（A1 --> A2 --> A3）
    - A1: Jingdong，何宁
    - A2: 维亮，马丽
    - A3: 远超，晓娅
3. 轮值小组的职责为：
    - 与大家协调时间，并预定会议室
    - 负责当周的沙龙内容主讲
    - 维护此Git repo，包括添加沙龙内容，添加Gist内容，维护沙龙列表
    - 轮值小组每次主讲一人，其余人负责答疑
4. 每次沙龙需要提前准备好文档，以markdown形式同步与此git repo
5. 每周沙龙末尾，轮值小组A提出3个主题以备3周后的沙龙（可提前确认）
    - 主题内容要求与Amber团队工作强相关
    - 主题内容需要是纯技术类
    - 所有人可将自己感兴趣的主题更新到 [topic.md](https://github.com/duyuanchao/QF_Amber_TechWeekly/blob/master/topic.md)

## 文件夹结构说明
文件夹结构说明于下
```
.
├── README.md  # 沙龙说明
├── documents  # 详细文档文件夹
├── gist       # 短小代码或配置说明
└── topic.md   # 备选主题
```
其中gist文件夹可以存放一些代码片段（功能类似[Github Gist](https://gist.github.com/)），例如：
- 新安装的Ubuntu系统需要更新安装的内容（sh文件）
- 美团云/阿里云新购买GPU服务器需要的基础配置(sh文件)
- Mac/Ubuntu Oh-my-zsh配置
- Mac/Ubuntu Vim配置

## 沙龙列表

| 序号 | 日期 | 主题 | 小组成员 |
| - | :-: |:- | :-: |
| 18 |20181026|[ python并行与并发 ](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/) | 远超 |
| 17 |20181019|[ 强化学习框架 ](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/) | 靖东 |
| 16 |20181012|[ Openface开源工具 ](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/) | 维亮 |
| 15 |20180914|[Numpy高级技巧](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/)<br>[Linux开机流程](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/) | 春上<br>于坤 |
| 14 |20180907|[python 内存管理](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/python_memory_control.md) | 远超 |
| 13 |201808024|[Tensorflow Server部署](https://github.com/qingfan-amber/weekly-tech-salon/)<br>[Go语言简介](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/Go%E8%AF%AD%E8%A8%80%E7%BC%96%E7%A8%8B.pdf) | 靖东<br>维亮 |
| 12 |201808017|[TensorRT](https://github.com/qingfan-amber/weekly-tech-salon/) | 春上 |
| 11 |201808010|[Celery简介](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/celery_intro.md) | 远超 |
| 10 |20180803|[GAN网络介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/GAN.pdf)<br>[深度学习面部情感计算综述](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/Deep%20Facial%20Expression%20Recognition-%20A%20Survey.pdf) | 靖东<br>维亮 |
| 09 |20180727|[pyAudioAnalysis说话人识别介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/pyAudioAnalysis_speaker_diarization.md)<br>[车牌识别](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/car_recognition.pdf) | 远超<br>王玥 |
| 08 |20180724|--- [模型裁剪](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/Pruning%20Introduction.pdf)<br>[VAD Introduce](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/introduction_of_VAD.pdf)| 春上<br>繁恺 |
| 07 |20180713|[EmotioNet介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/EmotioNet.pdf) <br>[EmotioNet Challenge介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/EmotioNet%20Challenge.pdf) | 维亮 |
| 06 |20180629|[maskrcnn介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/mask.pdf) | Jingdong |
| 05 |20180629|[Python Tips Logging](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/python_tips_logging.md) [Python Tips cProfile](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/python_tips_cprofile.ipynb)  | 远超 |
| 04 |20180622|[google 说话人分离论文](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/%E3%80%8C%E9%B8%A1%E5%B0%BE%E9%85%92%E4%BC%9A%E6%95%88%E5%BA%94%E3%80%8D%EF%BC%9A%E4%B8%80%E4%B8%AA%E9%9F%B3%E9%A2%91-%E8%A7%86%E8%A7%89%E8%AF%AD%E9%9F%B3%E5%88%86%E7%A6%BB%E6%A8%A1%E5%9E%8B.pdf)  | 繁恺 |
| 03 |20180615|[人脸识别算法介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/ArcFace%E8%AE%BA%E6%96%87.pdf) <br>[docker介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/Docker%E6%80%BB%E7%BB%93.md) | 马丽 <br> 维亮 |
| 02 | 20180608|[tensorflow的Keras接口](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/keras-JD.pdf)<br> [Free_standing会议的情感计算](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/affective_free_standing_conversation.md)| Jingdong <br> 远超 |
| 01 | 20180601|[LSTM介绍](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/lstm-understanding-applications.pdf)<br> [Attention is All You Need](https://github.com/qingfan-amber/weekly-tech-salon/blob/master/documents/attention%20is%20all%20you%20need.md)| 晓娅 <br> 繁恺 |
