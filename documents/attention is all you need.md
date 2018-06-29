# Attention is all you need 基于注意力机制的 Seq2Seq 模型

负责人: 曾繁恺

## 项目介绍

- **实验室** : Google Brain, Google Research, University of Toronto

- **文章影响力** : 该论文于 2017 年 12 月发布, 发布后, 文章中所构建的 Transformer 的模型引起世界范围内广泛讨论. 

- **工作简述** : 在 Transformer 的模型中, 完全摒弃 RNN, LSTM 的构架, 利用 attention 机制, 进行*序列到序列*的任务的处理.
    - **Scaled Dot-Product Attention** : Attention(Q,K,V)
    - **multi-head attention** : 多"角度"的atttention 结合, 使得对信息的关注更全面.
    - **Positional Encoding** : 弥补纯注意力模型中对于位置信息的缺失的短板.

- **主要贡献** : 
    1. 提出了新的 sequence to sequence 的模型
    2. 该模型框架未应用一般的 RNN, LSTM 构架, 降低的训练成本和难度
    3. 该模型提出的基于注意力机制的想法, 在自然语言处理(NLP)上, 是一种更接近与人类思考的方式.

- **关联知识** : 
    - **Feed-Forward Networks** : 模型构建中用到了基本的前馈神经网络.
    - **Adam optimizer** : 模型优化参数的主要方法
    - **数据集**: WMT 2014 English-to-German, WMT 2014 English-to-French
    - **tensor2tensor** : [tensor2tensor 库](https://github.com/tensorflow/tensor2tensor) 被本文作者团队用于训练和评估模型
    - **现有的其他 sequence to sequence 模型** : Extended Neural GPU, [ByteNet](https://arxiv.org/abs/1610.10099), [ConvS2S](https://arxiv.org/abs/1705.03122)

## 项目思路

### 源起

#### 经典的 sequence to sequence 模型

经典的解决诸如机器翻译等 sequence to sequence 的问题中, 常使用到的是 LSTM (Long and short term memory). 是 RNN 中的一种. 其处理问题的有效关键就在于 "Gate".

在 LSTM 中有一个称为 forget get 的单元, 其数值越接近于0, 则对于历史信息倾向于"遗忘", 其数值越接近于1, 则对于历史信息倾向于"记住". 这其实就是一种对于信息的"注意".

#### Transformer 模型

在经典的 Seq2seq 模型中, **注意力机制**(attention mechanism) 扮演了重要的角色, 所以这篇文章团队提出, 可以考虑单纯基于注意力机制来构建一个 Seq2seq 模型. 这就是 Transformer 的想法来源.

### 模型构架

**Encoder and Decoder Stacks**(编解码层) :

**Attention** : 
- Attention function: 用于将用于将一个序列与一系列键值对映射到一个输出中
    - Scaled Dot-Product Attention : 其实就是一个线性映射函数
    - **Multi-Head Attention** : queries, keys & values 通过不同的线性映射分别得到不同的相应的结果. 也就是说通过不同的"角度"去"关注"序列, 然后将这些结果组合在一起. 当 head 过多的时候, 会出现"过度关注"的情况, 而 head 过少, 则可能出现结果不准确的情况. 本文通过实践检验, 在机器翻译任务上, head_number = 6 是最佳值.
    - **self-attention** : 这是文章重点.基于attention的翻译模型，都需要在编码器和解码器两个部分分别刻画源句子和目标句子每个位置的信息，而刻画的信息需要同时包含单点信息和局部乃至全局信息。self-attention直接对词对信息加权拿到全局信息，理论上是一次计算。实际上，只做一次就只有朴素的词对组合信息了，所以会多做几次拿到更高级的组合。但无论如何，这个组合的程度是独立于序列长度的。而rnn想拿到头尾的组合，信息传递路径跟长度相关。
    - Position-wise Feed-Forward Networks : 在每一个 attention 子层都包含有一个全连接的基于位置的前馈神经网络.
    - **Positional Encoding** : 弥补纯注意力模型中对于位置信息的缺失的短板. 通过所谓"位置向量", 将每个位置编号, 然后每个编号对应于一个向量, 通过结合位置向量和词向量, 给每个词引入了相应的位置信息. 值得注意的是, 本文所定义的位置向量, 利用的三角函数. 本身 Positional Encoding 是绝对位置, 而通过三角函数表示的位置向量, 提供了相对位置的表达方式.

## 启发/应用前景

- 更加贴近人类自然思维的模型
- 机器翻译质量的提升, 更精准的语义/情绪识别
- 应用于辅助教学上, 教学内容关键点的提取和总结

## 更多相关资源

- [The Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html)
- [Translation with a Sequence to Sequence Network and Attention](https://pytorch.org/tutorials/intermediate/seq2seq_translation_tutorial.html?highlight=encoder)
