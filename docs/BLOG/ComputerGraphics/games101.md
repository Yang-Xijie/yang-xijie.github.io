---
title: GAMES101笔记
---

# GAMES101笔记

## Overview of Computer Graphics (L1)

## Review of Linear Algebra (L2)

## Transformation - 2D (L3)

### 逆时针旋转 $\theta$

$R_\theta = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$

$R_\theta = R_{-\theta} = R_\theta^T$

### Homogenous Coordinates

- 2D point $\begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$
- 2D vector $\begin{pmatrix} x \\ y \\ 0 \end{pmatrix}$
- $\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} a & b & t_x \\ c & d & t_y \\ 0 & 0 & 1 \end{pmatrix} \cdot \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$
- $\begin{pmatrix} x \\ y \\ w \end{pmatrix} = \begin{pmatrix} x/w \\ y/w \\ 1 \end{pmatrix}$ 表示一个二维点
- 两点相加得到中点

### 变换叠加

$M \begin{pmatrix} x \\ y \\ 1 \end{pmatrix} = A_n \cdots A_2 A_1 \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$ 

## Transformation - 3D (L4)

### 三维旋转

$R_{xyz}(\alpha,\beta,\gamma) = R_x(\alpha) R_y(\beta) R_z(\gamma)$

头：上下看 pitch 左右转 yaw 向日葵歪头 roll

Rodrigues’ Rotation Formula

绕轴 $\vec{n}$ 旋转 $\alpha$：$R(\vec{n}, \alpha) = \cos \alpha \cdot I + (1 - \cos\alpha) \cdot \vec{n} \vec{n}^T+\sin \alpha \cdot \begin{pmatrix} 0 & -n_{z} & n_{y} \\ n_{z} & 0 & -n_{x} \\ -n_{y} & n_{x} & 0 \end{pmatrix}$

四元数：为了解决旋转矩阵的插值问题

### MVP

model view projection

#### 相机

相机：位置 $\vec{e}$ 正对的方向 $\hat{g}$ 朝上的方向 $\hat{t}$

把相机放到 $(0,0,0)$ 正对 $-z$ 方向 头顶为 $y$ 方向

$M = R \cdot T$ 表示先将相机放到原点 然后把相机的方向旋转到上述方向

$M = R \cdot T = (R^{-1})^{-1} \cdot T = \begin{bmatrix} x_{\hat{g}\times \hat{t}} & x_t & x_{-g} & 0 \\ y_{\hat{g}\times \hat{t}} & y_t & y_{-g} & 0 \\ z_{\hat{g}\times \hat{t}} & z_t & z_{-g} & 0 \\ 0 & 0 & 0 & 1  \end{bmatrix}^T \cdot \begin{bmatrix} 1 & 0 & 0 & -x_e \\ 0 & 1 & 0 & -y_e \\ 0 & 0 & 1 & -z_e \\ 0 & 0 & 0 & 1 \end{bmatrix}$

#### 正交投影

将原空间放到原点 再在三个轴上缩放到 $[-1, 1]$

top/bottom n(靠前的面 成像位置)/f(靠后的面 实际位置) left/right

$M=\begin{bmatrix} \frac{2}{r-l} & 0 & 0 & 0 \\ 0 & \frac{2}{t-b} & 0 & 0 \\ 0 & 0 & \frac{2}{n-f} & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}\begin{bmatrix} 1 & 0 & 0 & -\frac{r+l}{2} \\ 0 & 1 & 0 & -\frac{t+b}{2} \\ 0 & 0 & 1 & -\frac{n+f}{2} \\ 0 & 0 & 0 & 1 \end{bmatrix}$

#### 透视投影

先将平面缩放到与期望的画布同大小 类似相似三角形 然后$z$对应的矩阵行用待定系数法确定 $M = \begin{bmatrix} n & 0 & 0 & 0 \\ 0 & n & 0 & 0 \\ 0 & 0 & n+f & -nf \\ 0 & 0 & 1 & 0 \end{bmatrix}$

做完这一步之后再使用正交投影将$f$处的画面拉到$n$处即可

## Rasterization - Triangles (L5)

MVP做完之后我们会得到一个 $[-1,1]^3$ 的规范立方体

首先将这个立方体变换到 $[0,width],[0,height],[-1,1]$

$M = \begin{bmatrix} w/2 & 0 & 0 & w/2 \\ 0 & h/2 & 0 & h/2 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$

然后要将三角形变到像素（这里暂时不考虑深度）

```
for pixel in image {
    pixel.toRasterize = isInside(triangle, pixel.centerX, pixel.centerY)
}
```

`isInside()`的实现：判断三角形三边与要判断的点的关系

$\overrightarrow{AP} \times \overrightarrow{AB},\overrightarrow{BP} \times \overrightarrow{BC},\overrightarrow{CP} \times \overrightarrow{CA}$ 的结果同向

加速光栅化：不对所有的像素遍历 只遍历可能的像素

## Rasterization - Antialiasing (L6)

走样 - alias：以同一种频率采样两种不同频率的信号得到相同的结果

不希望看到的结果 - artifacts

aliasing artifacts 采样的速度跟不上信号变化的速度

解决方案

- 提高屏幕分辨率
- 先对三角形做模糊将高频分量抑制 然后再采样（回忆时域卷积-频率相乘）
- MSAA(multi-sample) 将像素分割为小像素然后计算出颜色比例
- FXAA(fast-approximate) 对有锯齿的图形作后期处理
- TAA(temporal) 利用两帧之间的运动信息

其他：超分辨率 用深度学习模型来猜缺失的采样点

## Rasterization - Z-Buffer (L7)

画家算法

- 先画远处的东西 将近处的东西依次覆盖其上
- 对于三角形不适用

Z-Buffer

- 并行处理所有的三角形 光栅化后得到像素和深度
- 得到一个像素的深度后 和`depth buffer`存储的现有最小深度作比较 如果近的话 就将像素的颜色覆盖到`frame buffer`上

## Shading - Illumination (L7)

- shading - 着色/上色 主要考虑的是一个小三角形面的材质对光线的反射 是局部的
    - shading point 小面的中心点
    - $\hat{n}$ 小面的法向量 注意面有厚度/有里外
    - $\hat{l}$ 光线入射的方向
    - $\hat{v}$ camera的方向
- shadow - 阴影 考虑的是物体间的遮挡关系

shading 

- specular highlights - 高光 反射
- diffuse reflection - 漫反射 光线入射后从半球均匀射出
    - $L_d = k_d \frac{I}{r^2} \max(0,\hat{n}\cdot\hat{l})$
        - $L_d$ 漫反射的光强度
        - $k_d$ 漫反射系数 越大表示漫反射越强 也就是越亮
        - $\frac{I}{r^2}$ 点光源发出的光强平方衰减
        - $\cos\theta = \hat{n}\cdot\hat{l}$ 入射光线越倾斜 小面得到光强就越小
        - $\max(0,\hat{n}\cdot\hat{l})$ 考虑光线从物体后方入射 这时没有反射
- ambient lighting - 环境光 假定是常数
