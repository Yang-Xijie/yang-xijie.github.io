# 电路方程 | 二阶线性时不变电路方程列写及五要素法总结

## 列写方法

正规列写（用矩阵参量+端口定义写）；用基尔霍夫定律列写够两个方程

## 列写二阶微分方程

对于一个未知量，可以列写出一个二微分方程如下：

$\frac{d^{2}}{d t^{2}} x+a \frac{d}{d t} x+b x=s_{x}$

$\frac{d^{2}}{d t^{2}} x+2 \xi \omega_{0} \frac{d}{d t} x+\omega_{0}^{2} x=s_{x}$

其中$\omega_0$是自由振荡频率，$\xi$是阻尼系数

$a=2\xi\omega_0,\ b=\omega_0^2;\ \omega_0=\sqrt{b},\ \xi=\frac{a}{2\sqrt{b}}$

## 传递函数

$\frac{\dot{X}}{\dot{S}}=\frac{\dot{S}_ {X} / \dot{S}}{s^{2}+2 \xi \omega_{0} s+\omega_{0}^{2}},\ s=j\omega$

- 典型二阶低通：$H_{C}(s)=\frac{\dot{V}_ {C}}{\dot{V}_ {S}}=\frac{\omega_{0}^{2}}{s^{2}+2 \xi \omega_{0} s+\omega_{0}^{2}}$
- 典型二阶带通：$H_{R}(s)=\frac{\dot{V}_ {R}}{\dot{V}_ {S}}=\frac{2 \xi \omega_{0} s}{s^{2}+2 \xi \omega_{0} s+\omega_{0}^{2}}$
- 典型二阶高通：$H_{L}(s)=\frac{\dot{V}_ {L}}{\dot{V}_ {S}}=\frac{s^{2}}{s^{2}+2 \xi \omega_{0} s+\omega_{0}^{2}}$

## 解的形态

特征方程：$\lambda^{2}+2 \xi \omega_{0} \lambda+\omega_{0}^{2}=0$

- $\xi=0$无阻尼，理想正弦振荡
- $0<\xi<1$欠阻尼，特征方程有两个共轭复根（左半平面）$\lambda_{1,2}=\left(-\xi \pm j \sqrt{1-\xi^{2}}\right) \omega_{0}$，幅度指数衰减的正弦振荡
- $\xi=1$临界阻尼，特征方程有两个负实重根，
- $\xi>1$过阻尼，特征方程有两个负实根$\lambda_{1,2}=\left(-\xi \pm \sqrt{\xi^{2}-1}\right) \omega_{0}$，指数衰减

## 求解方法：待定系数法

$x(t)=x_{\infty}(t)+\left\{\begin{array}{lr}A e^{\lambda_{1} t}+B e^{\lambda_{2} t} & \xi>1 \\ A e^{-\omega_{0} t}+B t e^{-\omega_{0} t} & \xi=1 \\ e^{-\xi \omega_{0} t}\left(A \cos \sqrt{1-\xi^{2}} \omega_{0} t+B \sin \sqrt{1-\xi^{2}} \omega_{0} t\right) & 0<\xi<1\end{array}\right.$

其中：$\lambda_{1,2}=\left(-\xi \pm \sqrt{1-\xi^{2}}\right) \omega_{0}$；A、B为待定系数，由电路初始状态$x(0^+)\ \frac{d}{dt}x(0^+)$决定

## 求解方法：五要素法

三要素：稳态响应$x_\infty(t)$、阻尼系数$\xi$和自由振荡频率$\omega_0$、初值和微分初值$x(0^+)\ \frac{d}{dt}x(0^+)$

### 稳态响应

使用向量法求解。直流时利用电容电感高频低频特性求解。

### 阻尼系数和自由振荡频率

#### 特殊：RLC串联与GCL并联

自由振荡频率均为$\omega_0=\frac{1}{\sqrt{LC}}$

阻尼系数：RLC串联$\xi=\frac{R}{2Z_0}=\frac{R}{2\sqrt{\frac{L}{C}}}$，RCL并联$\xi=\frac{G}{2Y_0}=\frac{1}{2R\sqrt{\frac{C}{L}}}$

#### 一般：从传递函数推导

$H(j \omega) \stackrel{j \omega \rightarrow s}{=} \frac{? ? ?}{s^{2}+2 \xi \omega_{0} s+\omega_{0}^{2}}$

将分母中$s^{2}$的系数归一化，然后观察一次项和零次项的系数，得到$\xi\ \omega_0$

#### 一般：从二阶微分方程推导

$\frac{d^{2}}{d t^{2}} x+a \frac{d}{d t} x+b x=s_{x}$

$\frac{d^{2}}{d t^{2}} x+2 \xi \omega_{0} \frac{d}{d t} x+\omega_{0}^{2} x=s_{x}$

$a=2\xi\omega_0,\ b=\omega_0^2\Longrightarrow\omega_0=\sqrt{b},\ \xi=\frac{a}{2\sqrt{b}}$

### 写结果

#### $0<\xi<1$

复杂：$x(t)=x_{\infty}(t)+\left(X_{0}-X_{\infty 0}\right) e^{-\xi \omega_{0} t} \cos \sqrt{1-\xi^{2}} \omega_{0} t+\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\xi \omega_{0}}+X_{0}-X_{\infty 0}\right) \frac{\xi}{\sqrt{1-\xi^{2}}} e^{-\xi \omega_{0} t} \sin \sqrt{1-\xi^{2}} \omega_{0} t$

$x(t)=x_{\infty}(t)+ e^{-\xi \omega_{0} t} (A\cos \sqrt{1-\xi^{2}} \omega_{0} t+B \sin \sqrt{1-\xi^{2}} \omega_{0} t)$

$A=X_{0}-X_{\infty 0}$

$B=\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\xi \omega_{0}}+X_{0}-X_{\infty 0}\right) \frac{\xi}{\sqrt{1-\xi^{2}}}$

#### $\xi=1$

直接带入$\xi=1$得到：

复杂：$x(t)=x_{\infty}(t)+\left(X_{0}-X_{\infty 0}\right) e^{-\omega_{0} t}+\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\omega_{0}}+X_{0}-X_{\infty 0}\right) \omega_{0} t e^{-\omega_{0} t}$

$x(t)=x_{\infty}(t)+e^{-\omega_{0} t} \left [\left(X_{0}-X_{\infty 0}\right) +\left(\frac{\dot{X}_{0}-\dot{X}_{\infty 0}}{\omega_{0}}+X_{0}-X_{\infty 0}\right) \omega_{0} t \right]$

#### $\xi>1$

将欠阻尼$0<\xi<1$情况中的$\sqrt{1-\xi^{2}}$换成$\sqrt{\xi^{2}-1}$，$\cos\ \sin$换成$\cosh\ \sinh$

$x(t)=x_{\infty}(t)+ e^{-\xi \omega_{0} t} (A\cosh \sqrt{\xi^{2}-1} \omega_{0} t+B \sinh \sqrt{\xi^{2}-1} \omega_{0} t)$

$x(t)=x_{\infty}(t)+\left(X_{0}-X_{\infty 0}\right) e^{-\omega_{0} t}+\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\omega_{0}}+X_{0}-X_{\infty 0}\right) \omega_{0} t e^{-\omega_{0} t}$

复杂：$x(t)=x_{\infty}(t)+\left(X_{0}-X_{\infty 0}\right) e^{-\xi \omega_{0} t} \cosh \sqrt{\xi^{2}-1} \omega_{0} t+\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\xi \omega_{0}}+X_{0}-X_{\infty 0}\right) \frac{\xi}{\sqrt{\xi^{2}-1}} e^{-\xi \omega_{0} t} \sinh \sqrt{\xi^{2}-1} \omega_{0} t$

过阻尼：最后还需化简为两个指数衰减函数叠加的效果

得到：

$x(t)=x_{\infty}(t)+\frac{A+B}{2} e^{\lambda_{1} t}+\frac{A-B}{2} e^{\lambda_{2} t}$

其中：$\lambda_{1,2}=\left(-\xi \pm \sqrt{1-\xi^{2}}\right) \omega_{0}$

# 注

- $\sinh x=\frac{e^{x}-e^{-x}}{2}$
- $\cosh x=\frac{e^{x}+e^{-x}}{2}$
- $\sin x=\frac{e^{j x}-e^{-j x}}{2 j}$
- $\cos x=\frac{e^{j x}+e^{-j x}}{2}$

# 总结

## 稳态响应

使用向量法求解。直流时利用电容电感高频低频特性求解。

## 阻尼系数和自由振荡频率

### 特殊：RLC串联与GCL并联

自由振荡频率均为$\omega_0=\frac{1}{\sqrt{LC}}$

阻尼系数：RLC串联$\xi=\frac{R}{2Z_0}=\frac{R}{2\sqrt{\frac{L}{C}}}$，RCL并联$\xi=\frac{G}{2Y_0}=\frac{1}{2R\sqrt{\frac{C}{L}}}$

### 一般：从传递函数推导

$H(j \omega) \stackrel{j \omega \rightarrow s}{=} \frac{? ? ?}{s^{2}+2 \xi \omega_{0} s+\omega_{0}^{2}}$

将分母中$s^{2}$的系数归一化，然后观察一次项和零次项的系数，得到$\xi\ \omega_0$

## $0<\xi<1$

$x(t)=x_{\infty}(t)+ e^{-\xi \omega_{0} t} (A\cos \sqrt{1-\xi^{2}} \omega_{0} t+B \sin \sqrt{1-\xi^{2}} \omega_{0} t)$

$x(t)=x_{\infty}(t)+ e^{-\xi \omega_{0} t} \sqrt{A^2+B^2} \sin \left(\sqrt{1-\xi^{2}} \omega_{0} t+\arctan\frac{A}{B}\right)$

其中：$A=X_{0}-X_{\infty 0},\ B=\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\xi \omega_{0}}+X_{0}-X_{\infty 0}\right) \frac{\xi}{\sqrt{1-\xi^{2}}}$

## $\xi=1$

$x(t)=x_{\infty}(t)+e^{-\omega_{0} t} \left [\left(X_{0}-X_{\infty 0}\right) +\left(\frac{\dot{X}_ {0}-\dot{X}_ {\infty 0}}{\omega_{0}}+X_{0}-X_{\infty 0}\right) \omega_{0} t \right]$

## $\xi>1$

$x(t)=x_{\infty}(t)+\frac{A+B}{2} e^{\lambda_{1} t}+\frac{A-B}{2} e^{\lambda_{2} t}$

其中：$\lambda_{1,2}=\left(-\xi \pm \sqrt{\xi^{2}-1}\right) \omega_{0}$
