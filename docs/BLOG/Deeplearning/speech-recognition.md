# Speech Recognition 学习笔记

## 李宏毅 2020

[讲稿](http://speech.ee.ntu.edu.tw/~tlkagk/courses/DLHLP20/ASR%20%28v12%29.pdf)

- [1/7](https://www.youtube.com/watch?v=AIKu43goh-8) Overview
    - 语音识别：转语音为文本
        - 转语音为翻译
        - 从语音中提取意图
        - 从语音中提取重要信息
    - 语音：长度为T 维数为d 的一列向量
    - 文字：一列token：token的选取：
        - phoneme 语音的最小单位（使用较多）
        - graphme 文字的最小单位（使用较多）
        - word 文字中的词
        - morpheme 单词中的最小单位
        - btyes
        - UTF-8
    - 语音处理方式
        - 使用一个25ms的窗 每次前移10ms
            - 直接用音频幅度表示
            - 39维的MFCC
            - 80维的 filter bank（常用）
        - DFT
        - filter bank
        - log DCT
        - MFCC
    - 方法
        - HMM
        - seq2seq
    - 模型
        - LAS - Listen, Attend and Spell
        - CTC - Connectionist Temporal Classfication
        - LAS + CTC
        - RNN-T - RNN Transducer
        - HMM-hybrid 
        - Neural Transducer
        - MoChA - Monotonix Chunkwise Attention
- [2/7](https://www.youtube.com/watch?v=BdUeBa6NbXA) Listen, Attend, Spell
    - LAS模型详解 就是seq2seq
    - Listen
        - 提取特征
        - 做 down sampling
    - Attention
        - 考虑词语的前后关联
        - 最后做softmax给出一个联合概率分布
    - Spell
        - 结合前面的token给出现在的字符（这里的关联可以是多样的）
        - beam search - 只保留目前最好的b条路径
    - 训练过程
        - teacher forcing - 给数据进去的时候得是ground truth
    - 局限
        - 由于考虑token之间的关联 LAS听完一句话后才会给出结果 因此识别不是实时的
- [3/7](https://www.youtube.com/watch?v=CGuLuBaLIeI) CTC, RNN-T and more
    - CTC模型详解 decoder是线性分类器的seq2seq
        - 对每一个语音块输出一个结果（26个字母加phi）有 中间隔一个phi就分开 多个重复的则删掉
        - 问题：每一个都是独立的 因此相互关联小一点
        - 可以和LAS和CTC结合起来 LAS的encoder就是CTC
        - 训练的时候需要alignment - 穷举
    - RNN-T模型详解 输入一个东西输出多个
        - RNA model - Recurrent Neural Aligner 输入一个东西输出一个
            - CTC加上前一个token的信息
            - 一个输入输出多个token？当然可以把多个token定义为一个token
        - 看到一个输入 一直输出 直到模型觉得一个token结束
        - 训练的时候需要alignment - 穷举
            - 如果不看phi的话 就可以训练了 只考虑token就可以了
    - Neural Transducer 每次输入一个window的RNN-T
        - 有注意力机制 与window size无太大关系
    - MoChA window移动伸缩的Neural Transducer
        - 动态移动window
        - 相当于一个一个token移动window
- [4/7](https://www.youtube.com/watch?v=XWTGY_PNABo) HMM (optional)
    - HMM - Hidden Markov Model
    - $P(X|Y)$ Acoustic Model HMM
        - 考量 state sequence $P(X|S)$
        - triphone 比 phoneme 更细致 考虑前后关系
        - triphone 再分才是 state 
        - 对两个概率建模 p(transition) 相邻的音素 p(emission) 音素产生识别结果
        - state 太多了 tied-state subspace GMM
        - 哪一个状态对应到输出
    - $P(Y)$ Language Model
    - 如何结合deep learning DNN-HMM hybrid 完全end2end比较少 但应该会越来越多
    - 5%已经很低了 因为人类也是5%的错误 标注数据也会出错的 当然也只是在数据集上好 日常使用还是有问题的
- [5/7](https://www.youtube.com/watch?v=5SSVra6IJY4) Alignment of HMM, CTC and RNN-T (optional)
    - 回到end2end的技术
    - 本质上是让 $Y^* = arg \max \log P(Y|X)$ 最大
    - 讲了alignment的技术 我感觉有点太具体了
- [6/7](https://www.youtube.com/watch?v=L519dCHUCog) RNN-T Training (optional)
    - 总结
        - LAS考虑前后关系 训练简单 适用于长时语音识别
        - CTC和RNN-T 需要遍历alignment 训练时需要考虑所有alignment 适用于实时的语音识别
- [7/7](https://www.youtube.com/watch?v=dymfkWtVUdo) Language Modeling
    - LM: 估测 token sequence 出现的概率
        - BERT: 30亿以上的词 一个巨大的LM
        - 普通方法是直接数。
    - LAS: $T^* = arg \max P(Y|X) P(Y)$ 注意后面加的 $P(Y)$ 前面的比较难收集（需要时字典类的配对数据） 后面的很容易得到，数据量差的是数量级。这一点在别的模型上也会用。
    - N-gram LM: 整个token的几率可以被拆解为小的token的概率 N大概是看连着的几个词
        - 挑战：数据量不足以支持这样的统计 有些概率不是零的
        - 如果统计出来是0 应该给出0.0001（也可能是别的 LM smoothing）
    - wreck a nice beach | recognize speech
    - continuous LM: recommendation system
        - 从其他使用者的行为估计用户可能的行为 matrix factorization 本质上寻找的是用户之间的相似度
        - 类似的 可以寻找token的相似度 去估测概率为零的位置
        - 考虑背后隐藏的特征
        - emmm 不过后来还是被 deep learning 干掉了 深度学习还是很直觉的
    - NN-based LM / RNN-based LM
        - 想看多长的内容决定之后的内容
    - 用LM提升LAS
        - when to: 训练前后
        - how to: 隐藏层、输出

其他的一些想法：做深度学习 考虑好输入和输出的对应关系或函数关系

## 知乎

[陈孝良 语音识别技术简史](https://zhuanlan.zhihu.com/p/82872145)
