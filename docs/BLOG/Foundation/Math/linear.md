# 线性代数复习笔记

> 以清华大学林润亮老师的ppt为基础进行整理
> 
> 主要用来进行知识点回顾和快速复习

## 1 向量及其运算

### 线性代数

线性代数是建立在向量的 ` 加法 ` 和 ` 数乘 ` 这两种所谓 ` 线性运算 ` 上的

### 两向量相等

两个向量相等 $\iff$ 两者长度相等, 方向相同

### 向量运算性质

向量加法和数乘的运算性质: 交结零负一乘分分

分别是: 向量加法交换律, 向量加法结合律, 零向量, 反向量, 1 数乘向量, 两个数乘数乘向量, 两个数加数乘向量, 一个数数乘两个向量

### 列向量

$$
\vec{a}=
\begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_n
\end{pmatrix}
$$

其中 $a_i$ 为向量 $\vec{a}$ 的第 $i$ 个分量

### 向量的线性组合

设 $\vec v_1,\cdots,\vec v_m$ 为 $m$ 个 $n$ 维向量, 称 $c_1\vec v_1+\cdots +c_m\vec v_m$ 为向量 $\vec v_1,\cdots,\vec v_m$ 的一个线性组合

在 3 维空间中，一般，对于向量 $\vec u,\vec v,\vec w$

* {非零向量 $\vec u$} 的所有线性组合是一条直线;
* {不共线的 $\vec u,\vec v$} 的所有线性组合是一个平面;
* {不共面的 $\vec u,\vec v,\vec w$} 的所有线性组合是整个三维空间.

### 向量的长度

向量 $\vec v$ 的长度或模定义为 $\left\|\vec v\right \|=\sqrt{\vec v\cdot \vec v}$

### 向量正交

若 $\vec v\cdot \vec  w=0$, 则称向量 $\vec v$ 和 $\vec w$ 垂直 / 正交. 记作 $\vec v\perp \vec w$

### Cauchy-Schwarz 不等式

$|\vec v\cdot \vec w|=\left \|\vec v\right \|\left \|\vec w\right \|$, 等号成立当且仅当一个向量是另一个向量的倍数.

### 三角不等式

$\left\|\vec v+ \vec w\right \|\le \left\|\vec v\right\|+\left\|\vec w\right\|$, 等号成立当且仅当 $\vec v, \vec w$ 之一为另一向量的非负倍数.

## 2 矩阵与线性方程组

### 对矩阵与向量乘积的理解

$A \vec x$
- `理解1` 得到 $A$ 各列向量的一个线性组合;
- `理解2` 列向量 $\vec x$ 与 $A$ 各行向量做内积

### 对线性方程组的理解

$A \vec x=\vec b$
- `理解1` 求 $A$ 列向量的线性组合, 使之等于 $\vec b$;
- `理解2` 求向量 $\vec x$, 使之与 $A$ 的行向量内积分别为 $\vec b$ 中的元素

### 可逆矩阵

若 $A \vec x=\vec b$ ($n$ 个方程, $n$ 个未知数) 对任意向量 $\vec b$ 有唯一解, 则称方阵 $\vec A$ 可逆

若 $A=(\vec u, \vec v, \vec w)$ 可逆, 则 $\vec u, \vec v, \vec w$ 的全部线性组合所得空间是整个三维空间, 这时向量 $\vec u, \vec v, \vec w$ 线性无关 / 不共面, 相应 $A \vec x=\vec b$ 只有零解

### 线性方程组的行图和列图

`行图`(二维) 两直线交点
`列图`两列向量的线性组合

## 3 高斯消元法

### 矩阵的初等行变换

对方程组 $A \vec x=\vec b$, 消元法涉及以下三种同解变形:
1. 把一个方程减去另一个方程的倍数;
2. 交换两个方程的位置;
3. 用一个非零数乘一个方程.

相应地对增广矩阵作以下三种行变换 (即: 初等行变换):
1. 把一行减去另一行的倍数;
2. 交换两行;
3. 用一个非零数乘一行. 

### 增广矩阵

对线性方程组 $A \vec x=\vec b$ 做消元法, 即用一系列初等矩阵在左边, 去乘增广矩阵 $(A | \vec b)$

### 消去矩阵

将单位阵中某个 $0$ 变为非零的数得到的矩阵称为消去矩阵, 消去矩阵是一类初等矩阵

### 置换阵

如 $P_{12}=\begin{pmatrix} 0&1&0 \\ 1&0&0 \\ 0&0&1 \end{pmatrix}$

置换阵 $P$ 满足 $P^{-1}=P^{T}$

## 4 矩阵的运算

### 矩阵乘法的性质

满足结合律, 左分配律, 右分配律

矩阵的乘法一般不可交换, 消去律一般也不成立

### 分块矩阵

### 矩阵的转置

- 若 $A^T=A$ 则称 $A$ 是一个对称矩阵
- 若 $A^T=-A$ 则称 $A$ 是一个反对称矩阵
- 若 $R$ 为 $m\times n$ 矩阵 (实数域), 则 $RR^T$ 为 $m\times n$ 对称矩阵, 且其对角元均非负

## 5 矩阵的逆

### 逆矩阵

对方阵 $A$, 若存在矩阵 $B$, 满足 $AB=BA=I$, 则称 $A$ 是可逆的. 称 $B$ 是 $A$ 的逆矩阵, 记作 $A^{-1}$.

可逆矩阵也称为非奇异矩阵, 不可逆矩阵也称为奇异矩阵

### 性质

1. $n$ 阶阵 $A$ 可逆等价于 $A$ 有 $n$ 个主元
2. 方阵的逆唯一
3. 若 $A$ 可逆, 则 $A\vec x=\vec b$ 有唯一解 $\vec x=A^{-1}\vec b$
4. 若 $A\vec x=\vec 0$ 有非零解, 则 $A$ 不可逆
5. 二阶阵 $A=\begin{pmatrix} a&b \\ c&d \end{pmatrix}$ 可逆等价于 $ad-bc\neq0$, 且 $A^{-1}=\frac{1}{ad-bc}\begin{pmatrix} d&-b \\ -c&a \end{pmatrix}$
6. 对角阵可逆等价于对角元均不为 $0$
7. $(A^{-1})^{-1}=A$
8. $(AB)^{-1}=B^{-1}A^{-1}$

## 6 LU 分解

将矩阵分解成一个下三角矩阵和一个上三角矩阵的乘积

$EA=U, A=E^{-1}U=LU$

$A=E^{-1}DU=LDU$ 其中 $L$ 和 $U$ 的对角元为 $1$

### LU 分解的存在性和唯一性

设可逆矩阵 $A=(a_{ij})_{n\times n}$ 的顺序主子式 

$A_k = (a_{ij})_{k\times k}(k=1,\cdots ,n)$ 

均为可逆阵, 则 $A$ 有 $LU$ 分解. 

若 $l_{ii}=1, u_{ii}\neq 0(1\le i\le n)$, 则分解唯一

设 $A$ 是一个 $n$ 阶可逆阵, 则存在置换阵 $P$ 使得 $PA=LU$

### 对称矩阵的 $LDL^T$ 分解

## 7 向量空间

### 向量子空间

设 $V$ 是 $\mathbb R^n$ 的非空子集, 且 $V$ 关于向量加法和数乘运算封闭 ($\forall \alpha ,\beta\in V,\forall c_1,c_2\in \mathbb R \Longrightarrow c_1\alpha+c_2\beta\in V$), 则称 $V$ 是 $\mathbb R^n$ 的一个向量子空间

### 推广的向量空间的定义

在由称为“向量”的元素构成的非空集合 $V$ 中, 若定义了加法和数乘运算, 且对任意向量 $\vec{a}, \vec{b}, \vec{c}$ 及数域 $\mathbb{F}$, $k,l\in \mathbb{F}$ 满足以下八条性质:

1. $\vec a + \vec b=\vec b + \vec a$
2. $\vec a + (\vec b+\vec c)=(\vec a + \vec b)+\vec c$
3. 存在零向量 $\vec 0,\ \vec a+\vec 0=\vec a$
4. 对任意向量 $\vec a$, 存在唯一相反向量 $-\vec a$, 使得 $\vec a+(-\vec a)=\vec 0$
5. $1\cdot \vec a=\vec a$
6. $(kl)\vec a=k(l\vec a)$
7. $k(\vec a+\vec b)=k\vec a+k\vec b$
8. $(k+l)\vec a=k\vec a+l\vec a$

则称 $V$ 为定义在数域 $\mathbb{F}$ 上的向量空间

### 列空间

$A$ 的列向量所有线性组合构成的空间称为 $A$ 的列空间, 记作 $C(A)$

$C(A)=\{c_1 \vec \alpha_1+ c_2 \vec \alpha_2+\cdots+ c_n \vec \alpha_n | c_i\in \mathbb R\}=\{\vec y\in\mathbb R^m | \vec y=A \vec x,\vec x\in \mathbb R^n\}$

$A \vec x=\vec b$ 有解 $\iff \vec b\in C(A)$

求列空间: 将矩阵化为阶梯形, 阶梯形中主元所在的的列 / 原矩阵中主元所在的列的线性组合就是列空间

### 零空间

$N(A)=\{\vec x | A \vec x= \vec 0\}\subset \mathbb R^n$

求零空间: 将矩阵化为阶梯形 / 简化行阶梯形 (RREF), 将主元所在的列对应解 $\vec x$ 位置的数字标记为 1, 通过 $A \vec x=\vec 0$ 确定 $\vec x$ 其他位置的数字得到基础解系, 进行组合得到零空间

### 阶梯形

1. $A\overset{行变换}{\longrightarrow}U$, 则 $N(A)=N(U)$
2. $B \vec x= \vec 0\Longrightarrow AB \vec x= \vec 0$, 这说明 $N(B)\subset N(AB)$
3. $C(AB)\subset C(A)$, 即 $(AB)$ 的每一列是 $A$ 的列向量的线性组合
4. 设 $A \vec x=\vec b$ 有一个解 $\vec x^* $, 则 $A \vec x=\vec b$ 的解集为 $\vec x^*+N(A)$

## 8 求解齐次线性方程组

### $A \vec x=\vec 0$ 的基础解系
1. 主元个数 = 未知量个数 ($A$ 的列数)- 自由变量个数
2. 自由变量个数 = 基础解系中向量的个数 = 解集中线性无关解向量可达到的最大个数
3. 主元个数 = $A$ 的列向量中线性无关列向量的个数

## 9 求解非齐次线性方程组

### 极大线性无关组

向量组的极大线性无关组: 从原向量组中选出一部分向量构成的线性无关向量组, 并且再填入原向量组中的任一向量就线性相关

### 秩

向量组的秩: 向量组的极大线性无关组中向量的个数.

定理: 两组向量若能互相线性表出, 则它们的秩相等

$A$ 的行秩 = $A$ 的列秩 = $A$ 的秩

### 求特解 $\vec x^*$

将矩阵化为 RREF 后令自由变量为 0, 解出主元对应位置的数字即可

## 10 无关性、基与维数

### 基与维数

$\vec v_1, \vec v_2, \cdots , \vec v_n\in V$ 且 $\vec v_1, \vec v_2, \cdots , \vec v_n$ 线性无关, 且 $\forall \alpha\in V,\alpha$ 是 $\vec v_1, \vec v_2, \cdots , \vec v_n$ 的线性组合, 则称 $\{\vec v_1, \vec v_2, \cdots , \vec v_n\}$ 是 $V$ 的一组基

可逆矩阵与一组基相乘得到的还是一组基

### 关于秩的不等式

- $r(AB)\le \min \{r(A),r(B)\}$
- $r(A)=r(A^T)$
- $r(A+B)\le r(A)+r(B)$

## 11 四个基本子空间的基与维数

### 四个基本子空间

- 列空间 $C(A)=\{\vec y\in\mathbb R^m | \vec y=A \vec x,\vec x\in \mathbb R^n\}$
- 行空间 $C(A^T)=\{\vec y\in\mathbb R^n | \vec y=A^T \vec x,\vec x\in \mathbb R^m\}$
- 零空间 $N(A)=\{\vec x \in \mathbb R^n| A \vec x= \vec 0\}$
- 左零空间 $N(A^T)=\{\vec x \in \mathbb R^m| A^T \vec x= \vec 0\}$

- $C(A)$ 和 $N(A^T)$ 是 $\mathbb R^m$ 的子空间
- $C(A^T)$ 和 $N(A)$ 是 $\mathbb R^m$ 的子空间

### 子空间的基和维数

$RREF$ 中主元所在的列 / 对应原矩阵中的列是 $C(A)$ 的一组基

用 "上面行的倍数加到下面行" 化 $A$ 为阶梯形 (忽略中间的全零行), 阶梯形非零行标号对应 $A$ 的行即为 $C(A^T)$ 的一组基

- $A$ 的基础解系构成 $N(A)$ 的一组基
- $A^T$ 的基础解系构成 $N(A^T)$ 的一组基

- $dim(C(A))=dim(C(A^T))=r$
- $dim(N(A))=n-r$
- $dim(N(A^T))=m-r$

### 维数公式

$dim W_1+dim W_2=dim(W_1 \cap W_2)+dim(W_1+W_2)$

## 12 四个基本子空间的正交性

- $C(A^T)\perp N(A), C(A^T)+ N(A)=\mathbb R^n$
- $C(A)\perp N(A^T), C(A)+ N(A^T)=\mathbb R^m$

### $A \vec x=\vec b$ 在 $C(A^T)$ 中解的唯一性

定理: 若 $A \vec x=\vec b$ 有解, 则 $A \vec x=\vec b$ 在 $C(A^T)$ 中有唯一解

## 13 投影

### 引言

若 $A \vec x=\vec b$ 无解, 能够找到 $\hat{\vec x}\in \mathbb R^n$, 使得 $\left \| A \hat{\vec x}-\vec b \right \|$ 最小

直观上,$A \vec x=\vec b$ 无解 $\iff \vec  b\notin C(A)$. 上述问题意味着求 $C(A)$ 上距离 $\vec b$ 最近的点 $A\hat{\vec x}$, 它是 $\vec b$ 在 $C(A)$ 上的投影点

### 投影矩阵

点 $v$ 在平面 $\pi=C(A)$ 上的投影 $p$:

投影 $\vec p=A\hat{\vec x}\in C(A)\Longrightarrow \vec v- \vec p=\vec e\perp C(A) \Longrightarrow A^T(\vec v-A\hat{\vec x})=\vec 0$

$\Longrightarrow \hat{\vec x}$ 是 $A^TA \vec x=A^T \vec v$ 的解

若 $A$ 列满秩,$A^TA$ 是可逆阵 $\Longrightarrow \hat{\vec x}=(A^TA)^{-1}A^T \vec v, \vec p=A(A^TA)^{-1}A^T \vec v$

将 $P=A(A^TA)^{-1}A^T$ 称为投影矩阵

若 $A^TA$ 可逆, 投影阵 $P=A(A^TA)^{-1}A^T$ 满足 $P^2=P,P^T=P$

一般的, 一个矩阵 $P$ 满足 $P^2=P, P^T=P$, 则称 $P$ 为投影矩阵

## 14 最小二乘法

若 $A \vec x=\vec b$ 无解, 将 $A^TA\hat{\vec x}=A^T \vec b$ 称为正规方程组. 解出 $\hat{\vec x}$, 得到 $\vec b$ 在 C(A) 上的投影 $\vec p=A\hat{\vec x}$

## 15 Gram-Schmidt 正交化

目标: 给定 $V\in \mathbb R^n$ 为一个子空间,$\vec v_1,\vec v_2,\cdots ,\vec v_k$ 是 $V$ 的一组基, 把它们化成一组正交的向量 $\vec w_1,\vec w_2,\cdots ,\vec w_k$, 满足:
1. ${\vec w_i}^T\vec w_j=0,i\neq j$
2. $L(\vec v_1,\vec v_2,\cdots ,\vec v_t)=L(\vec w_1,\vec w_2,\cdots ,\vec w_t),1\le t\le k$,$L(\vec v_1,\vec v_2,\cdots ,\vec v_t)$ 表示 $\vec v_1,\vec v_2,\cdots ,\vec v_t$ 生成的 $V$ 的子空间

### 正交化过程

$$
\vec w_1=\vec v_1 \\
\vec w_2=\vec v_2-\frac{{\vec w_1}^T \vec v_2}{{\vec w_1}^T \vec w_1}\vec w_1 \\
\vec w_3=\vec v_3-\frac{{\vec w_1}^T \vec v_3}{{\vec w_1}^T \vec w_1}\vec w_1-\frac{{\vec w_2}^T \vec v_3}{{\vec w_2}^T \vec w_2}\vec w_2
$$

再进行单位化 $\vec q_i=\frac{\vec w_i}{\left \| \vec w_i \right \|}$

### QR 分解

举例:

$$
A=(\vec v_1,\vec v_2, \vec v_3)=\begin{pmatrix}1&1&0 \\ 1&0&1 \\ 0&1&1 \end{pmatrix}
$$

$$
A=QR=\begin{pmatrix} \frac{1}{\sqrt 2}&\frac{1}{\sqrt 6}&-\frac{1}{\sqrt 3} \\
\frac{1}{\sqrt 2}&-\frac{1}{\sqrt 6}&\frac{1}{\sqrt 3}\\0&\frac{2}{\sqrt 6}&\frac{1}{\sqrt 3} \end{pmatrix}\begin{pmatrix} \frac{2}{\sqrt 2}&\frac{1}{\sqrt 2}&\frac{1}{\sqrt 2} \\
0&\frac{3}{\sqrt 6}&\frac{1}{\sqrt 6}\\0&0&\frac{2}{\sqrt 3} \end{pmatrix}
$$

$R$ 是对角元为正数的上三角矩阵

## 16 行列式的基本性质

### 行列式的几何意义

- 二阶行列式的几何意义: 平面四边形的“有向”面积
- 三阶行列式的几何意义: 平行六面体的“有向”体积

### 行列式性质

1. 单位阵行列式为 $1$
2. 给一行乘 $c$, 行列式值乘 $c$
3. 一行元素可以拆为两数之和进而分为两个矩阵
4. 交换任意两行行列式值取反
5. 行列互换行列式值不变

推论:
1. 两行成比例, 行列式值为 $0$
2. 将一行的倍数加到另一行, 行列式值不变

### 行列式与初等变换

1. 行列式不为零等价于矩阵可逆
2. 两 $n$ 阶方阵乘积的行列式 = 各自行列式的乘积

## 17 行列式的计算

$M_{ij}$ 是 $A$ 划去第 $i$ 行第 $j$ 列得到的 $n-1$ 阶矩阵 

余子式: $\det M_{ij}$

代数余子式: $C_{ij}=(-1)^{i+j}\det M_{ij}$

### 行列式展开定理

$$
\det A=|{a_{ij}}|_ {n\times n}=a_ {i1}C_ {i1}+a_{i2}C_{i2}+\cdots+a_{in}C_{in},\forall i,j=1,\cdots,n
$$

### 典型计算方法

化为上三角或下三角, 计算对角元乘积即为行列式值

通过行列式展开定理展开进行不断降阶后计算行列式值

### n 阶范德蒙德行列式

$$ 
D_{n}=\left|\begin{array}{ccccc}
1 & 1 & 1 & \cdots & 1 \\
x_{1} & x_{2} & x_{3} & \cdots & x_{n} \\
x_{1}^{2} & x_{2}^{2} & x_{3}^{2} & \cdots & x_{n}^{2} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
x_{1}^{n-1} & x_{2}^{n-1} & x_{3}^{n-1} & \cdots & x_{n}^{n-1}
\end{array}\right|=\prod_{1 \leq i<j \leq n}\left(x_{j}-x_{i}\right)
$$

## 18 Cramer 法则及行列式的几何意义

### 代数余子式的重要性质

$$
\sum_{k=1}^{n}a_{ik}C_{jk}=\left\{\begin{array}{c}
D,i=j \\ 0,i\neq j
\end{array}
\right.
$$

### 伴随矩阵

下面的矩阵称为 $A$ 的伴随矩阵

$$
A^*=adj(A)=\left(\begin{array}{cccc}
C_{11} & C_{21} & \cdots & C_{n 1} \\
C_{12} & C_{22} & \cdots & C_{n 2} \\
\vdots & \vdots & & \vdots \\
C_{1 n} & C_{2 n} & \cdots & C_{n n}
\end{array}\right)
$$

$(A^*)^T$:$A$ 的代数余子式矩阵

### 求逆矩阵公式

$A^{-1}=\frac{adj(A)}{|A|}$

### 线性方程组的公式解

一般地, 若不使用行列式,$A$ 可逆时,$A \vec x=\vec b$ 解的表达式将非常复杂.

定理 (Cramer's Rule): 设 $A$ 是 $n$ 阶可逆阵,$\vec b \in \mathbb{R}^{n}$, 令 $B_{k}$ 是将 $A$ 的 第 $k$ 列换成向量 $\vec b$ 后所得的矩阵. 则 $A \vec {x}=\vec {b}$ 的唯一解为

$$
\vec {x}=\left(x_{1}, \cdots, x_{n}\right)^{T}, \quad x_{1}=\frac{\operatorname{det}\left(B_{1}\right)}{\operatorname{det} A}, \cdots, x_{n}=\frac{\operatorname{det}\left(B_{n}\right)}{\operatorname{det} A}
$$

### 向量的叉积 / 外积

$\vec u=\begin{pmatrix}u_1\\u_2\\u_3\end{pmatrix},\vec v=\begin{pmatrix}v_1\\v_2\\v_3\end{pmatrix}$,$\vec u\times \vec v$ 是与 $\vec u$ 和 $\vec v$ 都垂直且成右手关系的向量

有 $\vec u\times \vec v=-\vec v\times \vec u$

$(\vec u_1+\vec u_2)\times \vec v=\vec u_1\times \vec v+\vec u_2\times \vec v$

### 混合积

混合积 $\vec u\times \vec v\cdot \vec w$ , 几何上表示三向量组成的平行六面体的有向体积.

性质: $\vec u\times \vec v\cdot \vec w=\vec v\times \vec w\cdot \vec u=\vec w\times \vec u\cdot \vec v$

定理: $\vec u\times \vec v\cdot \vec w=\det (\vec u,\vec v,\vec w)$

## 19 特征值和特征向量

### 特征值

对 $A$, 若存在数 $\lambda$ 和非零向量 $\vec x$, 满足 $A \vec x=\lambda \vec x$, 则称 $\lambda$ 为 $A$ 的特征值,$\vec x$ 为 $A$ 的属于特征值 $\lambda$ 的特征向量数 $\lambda$ 为方阵 $A$ 的特征值 $\iff \det (A-\lambda I)=0$

$\det (A-\lambda I)=0$ 是关于 $\lambda$ 的多项式, 求解多项式得到 $\lambda$, 之后将解出的 $\lambda$ 分别带回 $(A-\lambda I)\vec x=\vec 0$ 即可解出特征值对应的特征向量

举例: 投影矩阵的特征值是 $0$ 和 $1$

### 特征值的性质

$\sum_{i=1}^{n}\lambda_i=tr(A)=\sum_{i=1}^{n}a_{ii}$

$\prod_{i=1}^n=\det A$

## 20 矩阵的对角化

设 $n\times n$ 矩阵 $A$ 有 $n$ 个线性无关的特征向量 $\vec x_1 ,\vec x_2,\cdots, \vec x_n, A \vec x_i=\lambda_i \vec x_i$, 令 $S=(\vec x_1 ,\vec x_2,\cdots, \vec x_n)$, 则 $S^{-1}AS$ 是一个对角矩阵 $\Lambda$, 其对角元素是 $A$ 的特征值
$$S^{-1}AS=\Lambda=\begin{pmatrix}\lambda_1& & \\ & \ddots& \\ & &\lambda_n\end{pmatrix}$$

若存在可逆矩阵 $S$, 使得 $S^{-1}AS$ 为对角矩阵, 则称矩阵 $A$ 是可对角化的

$n\times n$ 矩阵 $A$ 可对角化的充要条件是 $A$ 有 $n$ 个线性无关的特征向量 $\vec x_1 ,\vec x_2,\cdots, \vec x_n, A \vec x_i=\lambda_i \vec x_i$

定理:

设 $\vec \lambda_1 ,\vec \lambda_2,\cdots, \vec \lambda_k$ 是 $A$ 的互异特征值,$\vec x_1 ,\vec x_2,\cdots, \vec x_k$ 是相应特征向量, 则 $\vec x_1 ,\vec x_2,\cdots, \vec x_k$ 线性无关

推论:

具有 $n$ 个两两互异特征值的 $n\times n$ 矩阵可以对角化

### 特征值的代数重数和几何重数

定义: 设 $\operatorname{det}(A-\lambda I)=\left(\lambda_{1}-\lambda\right)^{n_{1}} \cdots\left(\lambda_{k}-\lambda\right)^{n_{k}}$, 其中 $\lambda_{i} \neq \lambda_{j}(i \neq j)$. 称 $n_{i}$ 为特征值 $\lambda_{i}$ 的代数重数, 记作 $AM\left(\lambda_{i}\right)=n_{i}$. 称 $\operatorname{dim} N\left(A-\lambda_{i} I\right)$ 为特征值 $\lambda_{i}$ 的几何重数, 记作 $G M\left(\lambda_{i}\right)=\operatorname{dim} N\left(A-\lambda_{i} I\right)$

$G M\left(\lambda_{i}\right)\le AM\left(\lambda_{i}\right)$

定理: 复方阵 $A$ 可对角化 $\iff$ 对任意特征值 $\lambda_i$ ,$G M\left(\lambda_{i}\right)= AM\left(\lambda_{i}\right)$

### 对角化的应用

快速计算 $A^k$

## 22 实对阵矩阵

- 定理: 实对称矩阵的特征值都是实数
- 定理: 任何实对称矩阵都正交相似于对角阵, 即对实对称阵 $A$, 存在正交阵 $Q$, 使 $Q^TAQ$ 为对角阵

## 1 正定矩阵

特征值全是正数的实对称矩阵称为正定矩阵

### 实对称矩阵 A 正定的充要条件

1. $A$ 的所有特征值均为正
2. ${\vec x}^TA \vec x>0$ 对所有非零实向量 $\vec x$ 成立
3. $A$ 的所有顺序主子式都是正的
4. (只做上面行的倍数加到下面行) $n$ 阶阵 $A$ 有 $n$ 个主元都是正的
5. 存在列满秩矩阵 $R$, 使得 $A=R^TR$
6. $A$ 的所有主子式都是正的

在 $n$ 阶行列式中任选 $k$ 行: 第 $i_1,i_2,\cdots,i_k$ 行, 再取相应的第 $i_1,i_2,\cdots,i_k$ 列. 由上述选取的 $k$ 行 $k$ 列交汇处元素组成的新矩阵称
为 $k$ 阶主子阵; 主子阵的行列式, 称为 $n$ 阶行列式的一个 $k$ 阶主子式.
在 $n$ 阶行列式中由第 $1,\cdots,k$ 行和第 $1,\cdots,k$ 列所确定的主子式称为 $k$ 阶顺序主子式.

### 半正定矩阵

若实对称矩阵 $A$ 的特征值均非负，那么称 $A$ 为半正定矩阵

### 半正定矩阵的判别条件

1. $A$ 的所有特征值 $\lambda_i$ 均非负
2. ${\vec x}^TA \vec x≥0$ 对所有实向量 $\vec x$ 成立.
3. 存在矩阵 $R$, 使得 $A=R^TR$ ($R$ 可能是不可逆阵)
4. A 的所有主子式均非负

### 二次型

对 $n$ 维实向量 $\vec x \in \mathbb R ^{n}$ 及 n 阶实矩阵 A, 称数值函数

$$
f(\mathbf{x})=\mathbf{x}^{T} A \mathbf{x}=\mathbf{x}^{T}\left(a_{i j}\right)_ {n \times n} \mathbf{x}=\sum_ {i=1}^{n} \sum_{j=1}^{n} a_{i j} x_{i} x_{j}
$$

为一个 (实) 二次型, 它是关于 $x_1,\cdots,x_n$ 的二次齐次多项式

### 主轴定理

设 $A$ 是一个 $n$ 阶实对称矩阵, 则存在正交变量代换 $\mathbf x = Q\mathbf y$, 使得二次型

$$
\mathbf{x}^{T} A \mathbf{x}=\mathbf{y}^{T} \Lambda \mathbf{y}=\sum_{i=1}^{n} \lambda_{i} y_{i}^{2}
$$

变为对角形的二次型, 其中 $Q^{T} A Q=\Lambda=\operatorname{diag}\left(\lambda_{1}, \cdots, \lambda_{n}\right)$, $\lambda_{1}, \cdots, \lambda_{n}$ 为 $A$ 的所有特征值.

### 二次型的分类

一个二次型 $f(\mathbf{x})=\mathbf{x}^{T} A \mathbf{x}$ 是:
* 正定的, 若对所有 $\mathbf{x} \neq \mathbf{0}$, 有 $f(\mathbf{x})>0$ $\iff A$ 的所有特征值都是正数
* 负定的, 若对所有 $\mathbf{x} \neq \mathbf{0}$, 有 $f(\mathbf{x})<0$ $\iff A$ 的所有特征值都是负数
* 不定的, 若 $f(\mathbf{x})$ 既有正值, 又有负值 $\iff A$ 既有正特征值, 又有负特征值
* 半正定的, 若对所有 $\mathbf x$, 有 $f(\mathbf{x}) \geq 0$
* 半负定的, 若对所有 $\mathbf x$, 有 $f(\mathbf{x}) \leq 0$

### 矩阵的合同

两个 $n$ 阶矩阵 $A$,$B$, 若存在 $n$ 阶可逆矩阵 $C$, 使得 $C^{T} A C=B$, 则称矩阵 $A$ 与 $B$ 合同, 记为 $A\cong B$ 

主轴定理可表述为: 任何实对称矩阵都正交合同于对角阵

## 3 奇异值分解

引言: 如何“对角化”$m\times n$ 矩阵

### 奇异值分解

设 $A$ 是一个 $m\times n$ 矩阵, 则存在 $m$ 阶正交矩阵 $U$ 和 $n$ 阶正交矩阵 $V$, 满足:

$$
A=U\begin{pmatrix}\sigma_1&&&\\&\ddots&&\\&&\sigma_2&\\&&&\vec 0\end{pmatrix}V^T=U\Sigma V^T
$$

其中 $r=rank(A)$. 习惯上, 取 $\sigma_1≥\sigma_2≥\cdots≥\sigma_r≥0$, 称 $\sigma_1, \sigma_2 ,\cdots,\sigma_r$ 为奇异值, 称 $U$ 和 $V$ 的前 $r$ 列向量为奇异向量. 这个分解称为奇异值分解, 简称 $SVD$.

有 $A \vec v_i=\sigma_i \vec u_i$,$A^T \vec u_i=\sigma_i \vec v_i$

有 $A^T A \vec v_i={\sigma_i}^2 \vec v_i$

$\vec u_i=\frac{A \vec v_i}{\sigma_i}$

- $\{\vec u_1, \cdots, \vec u_r\}$ 为 $C(A)$ 的一组单位正交基
- $\{\vec v_1, \cdots, \vec v_r\}$ 为 $C(A^T)$ 的一组单位正交基

### 奇异值分解的应用

设 $A=U\Sigma V^T$ 是 $m\times n$ 实矩阵 $A$ 的奇异值分解，$r=r(A)$, 则

* 正交矩阵 $U$ 的前 $r$ 列是 $C(A)$ 的一组标准正交基;
* 正交矩阵 $U$ 的后 $(m-r)$ 列是 $N(A^T)$ 的一组标准正交基;
* 正交矩阵 $V$ 的前 $r$ 列是 $C(A^T)$ 的一组标准正交基;
* 正交矩阵 $V$ 的后 $(n-r)$ 列是 $N(A)$ 的一组标准正交基.

## 4 线性变换 I

设 $V,W$ 是数域 $\mathbb F$ 上的向量空间,$V$ 到 $W$ 的映射 $T:V\to W$ 若保持加法和数乘计算, 即
$T(\vec x+ \vec y)=T(\vec x)+T(\vec y),\ T(k \vec x)=kT(\vec x), \ \forall \vec x,\vec y\in V,\ \forall k\in \mathbb F$, 则称 $T:V\to W$ 是一个线性变换

向量空间 $V$ 到 $W$ 的全体线性变换构成一个向量空间, 记为 $\mathcal L (V,W)$

### 线性变换的乘积

定义: 设 $\tau \in \mathcal{L}(U, V), \sigma \in \mathcal{L}(V, W) .$ 定义线性变换的乘积 $\sigma \tau: U \rightarrow W$ 为:

$$ 
(\sigma \tau)(\mathbf{u})=\sigma(\tau(\mathbf{u})), \quad \forall \mathbf{u} \in U
$$

直接验证得 $\sigma \tau \in \mathcal{L}(U, W)$

### 线性变换的逆

设 $\tau \in \mathcal{L}(V, V)$, 若存在 $\tau \in \mathcal{L}(V, V)$ 使得 $\sigma \tau=\tau \sigma=I$, 则称 $\sigma$ 是可逆线性变换, $\tau$ 为 $\sigma$ 的逆变换

### 线性变换的矩阵表示

$$
T\left(\mathbf{v}_ {1}, \ldots, \mathbf{v}_ {n}\right)=\left(T\left(\mathbf{v}_ {1}\right), \ldots, T\left(\mathbf{v}_ {n}\right)\right)=\left(\mathbf{w}_ {1}, \ldots, \mathbf{w}_ {m}\right)\left(\begin{array}{cccc}a_{11} & a_{12} & \cdots & a_{1 n} \\ a_{21} & a_{22} & \cdots & a_{2 n} \\ \vdots & \vdots & & \vdots \\ a_{m 1} & a_{m 2} & \cdots & a_{m n}\end{array}\right)
$$

称 $m\times n$ 矩阵 $A$ 为线性变换 $T$ 在 $V$ 中给定基 $\vec v_1,\cdots ,\vec v_n$ 和 W 中给定基 $\vec w_1,\cdots ,\vec w_m$ 下的矩阵表示

注: $A$ 中第 $j$ 列恰是 $T(\vec v_j)$ 在基 $\vec w_1,\cdots ,\vec w_m$ 下的坐标 '

定理: 设 $\vec v_1,\cdots ,\vec v_n$ 是 $n$ 维空间 $V$ 的一组基,$\vec w_1,\cdots ,\vec w_m$ 是 $m$ 维向量空间 $W$ 的一组基,$A$ 是任一 $m\times n$ 矩阵, 则有唯一的线性变换 $\sigma$ 满足:$\sigma (\vec v_1,\cdots ,\vec v_n)=(\vec w_1,\cdots ,\vec w_m)A$

## 5 线性变换 II

恒同变换: 对应矩阵 $I_n$

- 有线性变换 $\sigma:V\to W$
- 线性变换的核:$\ker \sigma=\{\vec v\in V | \sigma (\vec v)=\vec 0\}$
- 线性变换的像 (值域):$\operatorname{Im} \sigma = \{\sigma ( \vec v)|\vec v\in V\}$

- $\dim (\ker \sigma)$ 称为线性变换 $\sigma$ 的零度
- $\dim (\operatorname{Im} \sigma)$ 称为线性变换 $\sigma$ 的秩
