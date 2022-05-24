---
title: GAMES101笔记
---

# GAMES101笔记

## L1 Overview of Computer Graphics

## L2 Review of Linear Algebra

## L3 Transformation

### 逆时针旋转 $\theta$

$R_\theta = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$

### Homogenous Coordinates

- 2D point $\begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$
- 2D vector $\begin{pmatrix} x \\ y \\ 0 \end{pmatrix}$
- $\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} a & b & t_x \\ c & d & t_y \\ 0 & 0 & 1 \end{pmatrix} \cdot \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$
- $\begin{pmatrix} x \\ y \\ w \end{pmatrix} = \begin{pmatrix} x/w \\ y/w \\ 1 \end{pmatrix}$
- 两点相加得到中点

### 变换叠加

$M \begin{pmatrix} x \\ y \\ 1 \end{pmatrix} = A_n \cdots A_2 A_1 \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$ 

## L4 
