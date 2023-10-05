# 上帝视角看 GPU 笔记

做 GPGPU 计算的话，前三讲把该说的都说了，可以反复看的。

## 1 图形流水线基础

内存中的帧缓存，每 32 bit 表示一个像素。显卡作为图像的搬运工将图像显示到屏幕上。

shader（可编程流水线单元）

只要算法固定不变，都可以做成硬件。

GPU：解放 CPU。

## 2 逻辑上的模块划分

VertexShader 的计算结果可以写到内存中，而不是继续往后走流水线。

借用图形流水线做通用的并行计算，单入单出是一个限制。

有硬件支持的 GPGPU（只有计算流水线）：可以多入多出、可以任意读取、可以任意写入（UAV, Unordered Access View）。ComputeShader：输出输出都是内存

## 3 部署到硬件

VertexShader 和 PixelShader 结构越来越相似，形成 Unified Shader Architecture。通过动态调度解决负载平衡的问题。

GPU 与 CPU 的区别。

## 4 完整的软件栈

## 5 图形流水线中的不可编程单元

## 6 光线跟踪流水线
