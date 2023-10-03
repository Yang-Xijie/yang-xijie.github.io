# Gauss 公式和 Stokes 公式

# Gauss公式 | 基本形式

$$
\int_\Omega \nabla \cdot\vec F \ \text d\mu = \oint_{\partial\Omega} \vec F \cdot \text d\vec  \sigma
$$

## 三维空间

$$
\begin{aligned}
\int_\Omega \nabla \cdot\vec F\ \text d\mu &= \oint_{\partial\Omega} \vec F \cdot  \text d \vec\sigma 
\\
\int_\Omega \left( \frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z} \right) \text d\mu &= \oint_{\partial\Omega} \vec F \cdot \vec n\ \text d \sigma 
\\
\int_\Omega \left( \frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z} \right) \text dx\text dy\text dz &= \oint_{\partial\Omega} (P,Q,R) \cdot \vec n \ \text d \sigma 
\\
\int_\Omega \left( \frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z} \right) \text dx\text dy\text dz &= \oint_{\partial\Omega} P\text d y \text d z+Q\text d z \text d x+R\text d x \text d y
\end{aligned}
$$

## 平面

$$
\begin{aligned}
\int_D \nabla \cdot\vec F\ \text d\sigma &= \oint_{\partial D} \vec F \cdot \vec n\ \text d s
\\
\int_D \left( \frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}\right) \text d\sigma &= \oint_{\partial D} (P,Q)\cdot \vec n\ \text d s
\\
\int_D \left( \frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}\right) \text d x \text d y &= \oint_{\partial D} P\text d y-Q\text d x
\end{aligned}
$$

最后一式为Green公式的另一形式

# Stokes公式 | 基本形式

$$
\int_S \nabla \times \vec F \cdot \text d\vec\sigma = \oint_{\partial S} \vec F \cdot \text d \vec r
$$

## 三维曲面

$$
\begin{aligned}
\int_S \nabla \times \vec F \cdot \vec n\ \text d\sigma &= \oint_{\partial S} \vec F \cdot\text d \vec r
\\
\int_S 
\begin{vmatrix}
\vec{e_1} & \vec{e_2} & \vec{e_3}\\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z}\\
P & Q & R
\end{vmatrix} 
\cdot \vec n\ d\sigma &= \oint_{\partial S}(P,Q,R) \cdot \vec\tau\ \text d s
\\
\int_S 
\left(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z}\right) \text d y \text d z+
\left(\frac{\partial P}{\partial z}-\frac{\partial R}{\partial x}\right) \text d z \text d x+
\left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right) \text d x \text d y
&= \oint_{\partial S}P\text d x+Q\text d y+R\text d z
\end{aligned}
$$

## 平面

$$
\begin{aligned}
\int_D \nabla \times \vec F \cdot \vec n\ \text d \sigma &= \oint_{\partial D} \vec F \cdot  \text d \vec r
\\
\int_S 
\begin{vmatrix}
\vec{e_1} & \vec{e_2} & \vec{e_3}\\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z}\\
P & Q & 0
\end{vmatrix} 
\cdot (0,0,1)\ d\sigma &= \oint_{\partial S}(P,Q) \cdot \vec\tau\ \text d s
\\
\int_D 
\begin{vmatrix}
\frac{\partial}{\partial x} & \frac{\partial}{\partial y}\\
Q & R
\end{vmatrix} 
\text d \sigma &= \oint_{\partial D} (P,Q)\cdot \vec\tau\ \text d s
\\
\int_D \left( \frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)\text d x \text d y &= \oint_{\partial D} P\text d x+Q\text d y
\end{aligned}
$$

最后一式为Green公式的一般形式
