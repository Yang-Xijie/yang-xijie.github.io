# DDP 调研

## 什么是并行

- 深度学习的训练过程需要很多数据，比如商用的网络训练过程可能需要TB量级的数据，使用单GPU成为训练提速的瓶颈，人们希望能够使用一台机器上的多个GPU或多台机器上的多台GPU来加速训练过程。—— **数据并行**
- 深度学习的模型会有很多的参数，比如 `nn.Linear(10,10)` 就是110个参数，商用的网络模型参数甚至可能上百万千万，这些参数可能一台机器存不下，需要分布在多台机器。—— **模型并行**

事实上**模型并行比较少见**，目前来说，模型的参数远没有大到一台机器装不下的地步；**更需要关注的是数据的并行**来加速深度学习网络的训练过程。

更多关于并行的内容可以参见[PYTORCH DISTRIBUTED OVERVIEW](https://pytorch.org/tutorials/beginner/dist_overview.html)

## DP与DDP的区别

- [DP, torch.nn.DataParallel](https://pytorch.org/docs/stable/generated/torch.nn.DataParallel.html#torch.nn.DataParallel)
    - 实现了一台机器上的多GPU数据并行
    - 实质上是单进程 使用Python创建多线程 然后在线程间共享数据
        - 这样做的问题是[GIL of Python interpreter](https://realpython.com/python-gil/) 虽然确实数据分到了不同的GPU 但是CPU相当于只用了一个核 CPU这边可能会存在上限
    - （数据分批加载方式没有DDP智能）
    - **已经不会使用了**
- [DDP, torch.nn.parallel.DistributedDataParallel](https://pytorch.org/docs/stable/generated/torch.nn.parallel.DistributedDataParallel.html#torch.nn.parallel.DistributedDataParallel)
    - 实现了一台机器上的多GPU数据并行 也可以在多台机器上同时使用多个GPU训练
    - 实质上是创建了多个进程 每个进程对应一个GPU的训练。每个进程都有一个拷贝的model，在数据分配到进程时进行训练，训练结束后会将梯度更新到，所有进程共享的DDP_model，一次优化完毕后DDP_model再将新的model分发到每个进程的model

## DDP详解

见 [ddp-note.py](./ddp-note.md)

### DistributedSampler

[`torch.utils.data.distributed.DistributedSampler`](https://pytorch.org/docs/stable/data.html#torch.utils.data.distributed.DistributedSampler)

Usage:

```py
sampler = DistributedSampler(dataset) # DistributedSampler与DDP结合使用 这里DistributedSampler会将所有的数据分成world_size份 分别送入不同的进程/GPU
loader = DataLoader(dataset, shuffle=False, sampler=sampler) # 因为使用了sampler 所以shuffle可以关掉了
for epoch in range(start_epoch, n_epochs):
    if is_distributed:
        sampler.set_epoch(epoch) # 这里是为了让每个epoch 每台GPU上分到的数据分布不一样 相当于每个epoch都由DistributedSampler来重新将数据分组
    train(loader)
```

从[PyTorch多卡加速训练实际代码](https://github.com/inisis/bilibili-video/blob/main/Pytorch多卡加速训练/mnist_train_ddp.py)可以看到在深度学习基础的数据加载框架上包裹一个`DistributedSampler`并添加`sampler.set_epoch(epoch)`即可做到每轮每个GPU上的数据都不一样

### DataLoader

[什么是DataLoader](https://pytorch.org/tutorials/beginner/nn_tutorial.html#refactor-using-dataloader)

> DataLoader gives us each minibatch automatically.
> 
> `DataLoader`: Takes any `Dataset` and creates an iterator which returns batches of data.

## References

### PyTorch官方文档

基础是这一篇tutorial [PYTORCH DISTRIBUTED OVERVIEW](https://pytorch.org/tutorials/beginner/dist_overview.html#torch-nn-parallel-distributeddataparallel) 里面基本上所有的内容都说到了。

> [DDP notes](https://pytorch.org/docs/stable/notes/ddp.html) offer a starter example and some brief descriptions of its design and implementation. If this is your first time using DDP, start from this document.
> 
> [Getting Started with Distributed Data Parallel](https://pytorch.org/tutorials/intermediate/ddp_tutorial.html) explains some common problems with DDP training, including unbalanced workload, checkpointing, and multi-device models.

还有这一篇论文讲了DDP的具体实现 [PyTorch Distributed: Experiences on Accelerating Data Parallel Training](http://www.vldb.org/pvldb/vol13/p3005-li.pdf)

`DDP notes` 的配套代码是 `ddp-note.py` 可以在服务器上实际跑起来

### Bilibili

- [Bilibili - 蓝染惣右介灬 | PyTorch多卡加速训练（一）原理篇](https://www.bilibili.com/video/BV1Fb4y1r79A)
- [Bilibili - 蓝染惣右介灬 | PyTorch多卡加速训练（二）代码篇](https://www.bilibili.com/video/BV1so4y1Q7my)
    - 初始的深度学习代码基于[Bilibili - 蓝染惣右介灬 | 深度学习图像分类算法分享](https://www.bilibili.com/video/BV1xM4y1T7Sg)
    - [DP/DDP代码](https://github.com/inisis/bilibili-video/tree/main/Pytorch多卡加速训练)
