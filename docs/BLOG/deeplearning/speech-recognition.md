# Speech Recognition 学习笔记

## 李宏毅 2020

[讲稿](http://speech.ee.ntu.edu.tw/~tlkagk/courses/DLHLP20/ASR%20%28v12%29.pdf)

- [1/7](https://www.youtube.com/watch?v=AIKu43goh-8)
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
- [2/7](https://www.youtube.com/watch?v=BdUeBa6NbXA)
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
- [3/7](https://www.youtube.com/watch?v=CGuLuBaLIeI)
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
- [4/7](https://www.youtube.com/watch?v=XWTGY_PNABo)
- [5/7](https://www.youtube.com/watch?v=5SSVra6IJY4)
- [6/7](https://www.youtube.com/watch?v=L519dCHUCog)
- [7/7](https://www.youtube.com/watch?v=dymfkWtVUdo)

## 知乎

[陈孝良 语音识别技术简史](https://zhuanlan.zhihu.com/p/82872145)
