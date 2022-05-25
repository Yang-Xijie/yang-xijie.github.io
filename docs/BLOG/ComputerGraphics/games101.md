---
title: GAMES101笔记
---

# GAMES101笔记

## L1 Overview of Computer Graphics

## L2 Review of Linear Algebra

## L3 2D Transformation

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

## L4 3D Transformation

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
