# 动手学深度学习 笔记

<https://zh.d2l.ai/chapter_notation/index.html>

`Release 2.0.0-beta0` `d2l-zh-pytorch.pdf`

## 0 安装

```sh
conda create --name d2l python=3.8 -y # -y --yes Do not ask for confirmation.
conda activate d2l

pip install torch==1.8.1
pip install torchvision==0.9.1
pip install d2l==0.17.3
```

## 1.3 各种机器学习问题

有监督学习：

- 回归 regression 标签为实数 平方损失函数
- 分类 classification 标签为离散值 交叉熵损失函数

无监督学习：

- 你的老板可能会给你一大堆数据，然后让你用它做一些数据科学研究，却没有 对结果有要求
- 聚类(clustering)
- 主成分分析(principal component analysis)
- 因果关系(causality)和概率图模型(probabilistic graphical models)
- 生成对抗性网络(generativeadversarialnetworks)

## 2.7 查阅文档

https://pytorch.org/docs/stable/index.html

```py
print(dir(torch.distributions))
help(torch.ones)
```

## 3.1 线性回归

$\hat{y} = X w + b$

给定训练数据特征X和对应的已知标签y，线性回归的目标是找到一组权重向量w和偏置b:当给定从X的同分布中取样的新样本特征时，这组权重向量和偏置能够使得新样本预测标签的误差尽可能小。

模型质量的度量方式
能够更新模型以提高模型预测质量的方法

梯度下降通过不断地在损失函数递减的方向上更新参数来降低误差

梯度下降最简单的用法是计算损失函数(数据集中所有样本的损失均值)关于模型参数的导数(在这里也可以称为梯度)

## 3.2.7 训练

在每次迭代中，我们读取一小批量训练 样本，并通过我们的模型来获得一组预测。计算完损失后，我们开始反向传播，存储每个参数的梯度。最后， 我们调用优化算法sgd来更新模型参数。

## 3.3 使用PyTorch深度学习的高级框架来简化代码

可以背一下

```py
import numpy as np
import torch
from torch.utils import data
from torch import nn

true_w = torch.tensor([2, -3.4])  # 两个特征的权重
true_b = 4.2  # 偏置

learning_rate = 0.03
batch_size = 10
epoch_count = 3

# [1.生成数据集]


def create_data(w, b, sample_count):  # sample_count 样本量
    X = torch.normal(0, 1, (sample_count, len(w)))
    y = torch.matmul(X, w) + b  # y = Xw + b + noise
    y += torch.normal(0, 0.01, y.shape)
    return X, y.reshape((-1, 1))  # X 含有两个特征的样本 共sample_count行 # y 样本的值


features, labels = create_data(true_w, true_b, 1000)

# [2.读取数据集]


def create_iter(data_arrays, batch_size):
    """构造一个PyTorch数据迭代器"""
    dataset = data.TensorDataset(*data_arrays)
    return data.DataLoader(dataset, batch_size, shuffle=True)


data_iter = create_iter((features, labels), batch_size)

# [3.定义模型]

net = nn.Sequential(nn.Linear(2, 1))

# [4.初始化模型参数]

net[0].weight.data.normal_(0, 0.01)
net[0].bias.data.fill_(0)

# [5.定义损失函数]

loss = nn.MSELoss()

# [6.定义优化算法]

trainer = torch.optim.SGD(net.parameters(), lr=learning_rate)

# [7.训练]

for epoch in range(epoch_count):
    for X, y in data_iter:
        l = loss(net(X), y)
        trainer.zero_grad()
        l.backward()
        trainer.step()
    l = loss(net(features), labels)
    print(f"epoch {epoch + 1}, loss {l:f}")

w = net[0].weight.data
print("e(w)", true_w - w.reshape(true_w.shape))
b = net[0].bias.data
print("e(b)", true_b - b)
```
