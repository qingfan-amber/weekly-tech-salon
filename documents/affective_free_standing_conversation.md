# Free Standing Conversation 情感计算

负责人：远超

## 项目介绍

- **实验室**：University of Trento; ADSC, UIUC; Perugia

- **文章影响力：** 该工程一共包含3篇文章：
    - 本文ACM MultiMedia 2015Best Paper： [nalyzing Free-standing Conversational Groups: A Multimodal Approach](https://dl.acm.org/citation.cfm?id=2806238)
    - 介绍其数据集的文章，2015IEEE Trans. PAMI: [SALSA: A Novel Dataset for Multimodal Group Behavior Analysis](https://doi.org/10.1109/TPAMI.2015.2496269)
    - 头，体朝向预估(HBPE)：2015 ICCV（Oral）:[Uncovering Interactions and Interactors: Joint Estimation of Head, Body Orientation and F-formations from Surveillance Video](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Ricci_Uncovering_Interactions_and_ICCV_2015_paper.pdf)

- **工作简述：**
在Free Standing Conversation中，利用摄像头+可穿戴设备采集数据，进行分析。<br>

    - **多模态数据：** Visual; audio; infrared

    - **鲁棒性:** a).时序连续性（通过矩阵补全），b). 头身couping（2012 CVPR:[We are not contortionists: coupled adaptive learning for head and body orientation estimation in surveillance video]），c). Noise Inherent to the Scenario（Matrix Completion Model中包含noise regularization）

    - **分析目标：** F-formation; social attention attractors

- **主要贡献：**
1. 利用多信号（Multimodal）进行HBPE（head and body pose estimate）
2. 提出一个框架，能够不仅能够处理不同的信号，并且利用图像，语音，可穿戴设备来提取特征
3. 将HBPE问题转化为Matrix Completion问题，（补全红外光矩阵，以及声音矩阵）
4. 联合两个不完整的矩阵  进行Joint HBPE
5. 提出了一个新的方式进行matrix completion task （面向SALSA数据集）：计算F-formation 以及发现 social attention attractors


- **关联知识**
    - [F-formation](http://profs.sci.univr.it/~cristanm/ssp/)："An F-formation arises whenever two or more people sustain a spatial and orientational relationship in which the space between them is one to which they have equal, direct, and exclusive access."
    - Head and Body Pose Estimation
    - Sociometric Badges： [MIT Media Lab的可穿戴设备](http://hd.media.mit.edu/badges/)
    - [SALSA数据集](http://tev.fbk.eu/salsa)
    - social attention holding power(SAHP)

## 项目思路
### SALSA
18个参与者参加两个session：Poster Presentation & Cocktail。4个角落分别有4个摄像头，每人佩戴一个social badge(microphone, infrared beam and detector, USB Card ), 每3秒钟手动标注position, head and body orientation, F-formation

### Exprimental Setup
- visual feature for head and body ==> 多目标检测 ==> 在每个相机中框出head and body
    - [CVPR 2012] HOG discriptors 做出bounding box==> 框出head(20*20), body(80*80)==> 无重叠的4*4cell中提取HOG，==> 将4个视角想关联 **【用什么关联？】** ==> PCA降维（最终约为100维）
- Badges中的信息：==> 提取head and body pose labels(Section 3) ==> badges中的信息包含了参与者之间的关系（例：a. 如果person k的badge能够检测到person l，则可推断person k 是朝向person l的，因为badge是挂在胸前。b. 如果k的badge中的语音信号与l的语音信号强相关，则可能l是面向k的）
    - 将角度离散化，C=8，将360度分为8个朝向

### Head and body pose estimation
使用340帧图像（约17分钟）==> 提取到一个包含6120个head/body的样本集；==> 将其等分为2个数据集==> 利用一个来训练，其中10%的数据是手动标注，90%的数据是通过sociometric badges弱标注 ==> 总数据集为5%的数据为标注数据的稀疏标注数据集 ==> Figure 4展示了a)只用Ground Truth(GT)；b)GT + Audio; c). GT + infrared, d).all modalities的情况下进行Head and body estimation的准确率 ==> Table 对比了不同算法的分类精准度 **【另外几个算法是否有源代码？】**

### F-formation Detection
略

### Retrieving Social Attention attractors
找到人群中的social attention attractors是一个更高level的task。短期：可以找到谁在引领对话；中期：可以确定这个人在交流中的角色； 长期：表征人格。本文更关注长期的对话，从中可以找到poster的演讲者。==> 计算F-formation menbers朝向一个特定的人看。






## 启发思路
- 如何建立数据集，联系贾珈老师学生共同科研
- 有关于监控环境中，HBPE
- 有利用视频-音频联合分析的工作：Audio-Visual Speaker Diarization Based on
Spatiotemporal Bayesian Fusion
    - 法国科学院，Perception Group， 2018PAMI
- 多目标检测+Action Unit结合
- 根据4.5章节的描述，是否可以找到老师是谁
- 当前的课堂契合度可以深挖，哪个人会在第一时间引导课堂的情绪变化
