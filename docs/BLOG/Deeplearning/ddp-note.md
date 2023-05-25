# ddp-note.py

```py
# https://pytorch.org/docs/stable/notes/ddp.html
# This example uses a torch.nn.Linear as the local model, wraps it with DDP, and then runs one forward pass, one backward pass, and an optimizer step on the DDP model. After that, parameters on the local model will be updated, and all models on different processes should be exactly the same.

import torch
import torch.distributed as dist
import torch.multiprocessing as mp
import torch.nn as nn
import torch.optim as optim
from torch.nn.parallel import DistributedDataParallel as DDP
import os


def example(rank, world_size):
    """
    world_size: Number of processes participating in the job.
    rank: Rank of the current process (it should be a number between 0 and world_size-1).
    """

    # Initializes the default distributed process group
    dist.init_process_group("gloo", rank=rank, world_size=world_size)  # mpi, gloo, nccl
    # create local model
    model = nn.Linear(10, 10).to(rank)  # 这个model确实会每个rank（每个GPU）都创建一个
    # construct DDP model
    # This container parallelizes the application of the given module by splitting the input across the specified devices by chunking in the batch dimension. The module is replicated on each machine and each device, and each such replica handles a portion of the input. During the backwards pass, gradients from each node are averaged.
    # 这里虽然在每个进程上创建了一个model 但是由于DDP底层的实现 所以ddp_model在更新参数后都会变成一样的 或者说ddp_model是统一的
    ddp_model = DDP(model, device_ids=[rank])

    # define loss function and optimizer
    loss_fn = nn.MSELoss()
    optimizer = optim.SGD(ddp_model.parameters(), lr=0.001)

    # forward pass
    outputs = ddp_model(torch.randn(20, 10).to(rank)) # 这里需要给每个rank不同的数据进行训练 具体的训练过程中使用`DistributedSampler`
    labels = torch.randn(20, 10).to(rank)
    # backward pass
    # 梯度算自己的 但是算好之后ddp_model就知道算好了 当所有的进程都算好了之后 取个平均一更新就得到了总的参数下降
    # 这里的参数其实分了很多小组 每一个组都可以独立计算的
    # 得到平均的梯度之后分发给每一个local_model
    loss_fn(outputs, labels).backward()
    print(f"[{rank}] loss={loss_fn(outputs, labels)}")  # 可以看到loss是不一样的

    # update parameters
    # step过程相当于是给参数减去梯度 只是做减法的事情 而且由于梯度都已经同步 这一步是在当前process上的
    optimizer.step()
    for param in model.parameters():  # 打印进行验证 该线性层的weight和bias都是相同的
        print(f"[{rank}] param={param}")


def main():
    world_size = 2  # 需要创建的进程数

    # 创建进程 这个进程是fn函数 函数的第一个参数为进程序号i 其余参数用args给出
    # The function is called as fn(i, *args), where i is the process index and args is the passed through tuple of arguments.
    # nprocs: Number of processes to spawn.
    # join: Perform a blocking join on all processes. join指的是是否等待其他进程结束
    mp.spawn(fn=example, args=(world_size,), nprocs=world_size, join=True)


if __name__ == "__main__":

    # Environment Variable
    # We have been using the environment variable initialization method throughout this tutorial. By setting the following four environment variables on all machines, all processes will be able to properly connect to the master, obtain information about the other processes, and finally handshake with them.
    # MASTER_PORT: A free port on the machine that will host the process with rank 0.
    # MASTER_ADDR: IP address of the machine that will host the process with rank 0.
    # WORLD_SIZE: The total number of processes, so that the master knows how many workers to wait for.
    # RANK: Rank of each process, so they will know whether it is the master of a worker.

    # Environment variables which need to be set when using c10d's default "env" initialization mode.
    os.environ["MASTER_ADDR"] = "localhost"
    os.environ["MASTER_PORT"] = "29500"

    main()

# [输出结果]
# [0] loss=1.325094223022461
# [1] loss=1.1071380376815796
# [1] param=Parameter containing:
# tensor([[ 0.2285, -0.0826, -0.0155, -0.2931, -0.1031, -0.0244,  0.1876,  0.2748,
#           0.0449,  0.0260],
#         [-0.2138, -0.1442, -0.2235,  0.1534, -0.0009, -0.1772,  0.1886,  0.1407,
#          -0.1188,  0.1204],
#         [ 0.1479,  0.1675, -0.0642, -0.1608, -0.2220,  0.0374, -0.0347, -0.0370,
#          -0.1406, -0.2810],
#         [-0.1808, -0.1309,  0.2815,  0.2373, -0.1879,  0.2436,  0.1532, -0.1560,
#           0.1705,  0.1782],
#         [ 0.1426, -0.1456, -0.2564, -0.2116, -0.0984,  0.1470,  0.1768,  0.0492,
#           0.0377, -0.0393],
#         [ 0.0907,  0.0407, -0.1768,  0.0815, -0.0343, -0.0383, -0.1343,  0.1337,
#           0.1848,  0.0150],
#         [ 0.2765, -0.0645, -0.1146,  0.1858,  0.2048,  0.0912, -0.0023, -0.1567,
#           0.1289,  0.0228],
#         [ 0.0621, -0.2546,  0.1672, -0.2262, -0.2849, -0.2214, -0.1991, -0.0952,
#           0.1240, -0.1764],
#         [-0.1292,  0.0532, -0.1326, -0.0515, -0.0267, -0.1320, -0.2453, -0.1454,
#           0.0622, -0.2154],
#         [-0.1670,  0.0411,  0.2155, -0.2562, -0.2385, -0.2418, -0.0954,  0.0079,
#           0.0960,  0.2758]], device='cuda:1', requires_grad=True)
# [1] param=Parameter containing:
# tensor([-0.2487, -0.0690,  0.0535, -0.0476,  0.1599,  0.1830, -0.2424, -0.1128,
#          0.2034, -0.1532], device='cuda:1', requires_grad=True)
# [0] param=Parameter containing:
# tensor([[ 0.2285, -0.0826, -0.0155, -0.2931, -0.1031, -0.0244,  0.1876,  0.2748,
#           0.0449,  0.0260],
#         [-0.2138, -0.1442, -0.2235,  0.1534, -0.0009, -0.1772,  0.1886,  0.1407,
#          -0.1188,  0.1204],
#         [ 0.1479,  0.1675, -0.0642, -0.1608, -0.2220,  0.0374, -0.0347, -0.0370,
#          -0.1406, -0.2810],
#         [-0.1808, -0.1309,  0.2815,  0.2373, -0.1879,  0.2436,  0.1532, -0.1560,
#           0.1705,  0.1782],
#         [ 0.1426, -0.1456, -0.2564, -0.2116, -0.0984,  0.1470,  0.1768,  0.0492,
#           0.0377, -0.0393],
#         [ 0.0907,  0.0407, -0.1768,  0.0815, -0.0343, -0.0383, -0.1343,  0.1337,
#           0.1848,  0.0150],
#         [ 0.2765, -0.0645, -0.1146,  0.1858,  0.2048,  0.0912, -0.0023, -0.1567,
#           0.1289,  0.0228],
#         [ 0.0621, -0.2546,  0.1672, -0.2262, -0.2849, -0.2214, -0.1991, -0.0952,
#           0.1240, -0.1764],
#         [-0.1292,  0.0532, -0.1326, -0.0515, -0.0267, -0.1320, -0.2453, -0.1454,
#           0.0622, -0.2154],
#         [-0.1670,  0.0411,  0.2155, -0.2562, -0.2385, -0.2418, -0.0954,  0.0079,
#           0.0960,  0.2758]], device='cuda:0', requires_grad=True)
# [0] param=Parameter containing:
# tensor([-0.2487, -0.0690,  0.0535, -0.0476,  0.1599,  0.1830, -0.2424, -0.1128,
#          0.2034, -0.1532], device='cuda:0', requires_grad=True)
```
