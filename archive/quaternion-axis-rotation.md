# 四元数旋转表示转为欧拉角旋转表示

> 作者：杨希杰

## 起因

四元数 $q=(q_r, q_x, q_y, q_z)$ 可以表达一种旋转过程。绕三个坐标轴 xyz 旋转的角度也可以表达一种旋转过程 $\theta_x, \theta_y, \theta_z$，被称作欧拉角。理论上来说，这两种表达是可以相互转换的。

本文探究将四元数的旋转表示转为欧拉角的表示。

## 问题定义

某个点 $P$，写作四元数的表达形式 $q_P$，则该点先绕 x 轴旋转 $\theta_x$、再绕 y 轴旋转 $\theta_y$、最后绕 z 轴旋转 $\theta_z$ 后得到的点 $P'$ 为：

$$
q_{P'} = q_{\theta_z} q_{\theta_y} q_{\theta_x} q_P q_{\theta_x}^* q_{\theta_y}^* q_{\theta_z}^*
$$

对比点 $P$ 通过单个四元数 $q$ 旋转得到的点 $P'$：

$$
q_{P'} = q q_P q*
$$

想要构造出完全相同的旋转效果，需要：

$$
q = q_{\theta_z} q_{\theta_y} q_{\theta_x}
$$

其中：

$$
q = (q_r, q_x, q_y, q_z) \\
q_{\theta_x} = (\cos(\theta_x/2), \sin(\theta_x/2), 0, 0) \\
q_{\theta_y} = (\cos(\theta_y/2), 0, \sin(\theta_y/2), 0) \\
q_{\theta_z} = (\cos(\theta_z/2), 0, 0, \sin(\theta_z/2))
$$

代入上面的式子得到：

$$
\cos(\theta_x/2) \cos(\theta_y/2) \cos(\theta_z/2) + \sin(\theta_x/2) \sin(\theta_y/2) \sin(\theta_z/2) = q_r \\
\sin(\theta_x/2) \cos(\theta_y/2) \cos(\theta_z/2) - \cos(\theta_x/2) \sin(\theta_y/2) \sin(\theta_z/2) = q_x \\
\cos(\theta_x/2) \sin(\theta_y/2) \cos(\theta_z/2) + \sin(\theta_x/2) \cos(\theta_y/2) \sin(\theta_z/2) = q_y \\
\cos(\theta_x/2) \cos(\theta_y/2) \sin(\theta_z/2) - \sin(\theta_x/2) \sin(\theta_y/2) \cos(\theta_z/2) = q_z
$$

简写为：

$$
C_xC_yC_z + S_xS_yS_z = q_r \ (F_{00}) \\ 
S_xC_yC_z - C_xS_yS_z = q_x \ (F_{01}) \\
C_xS_yC_z + S_xC_yS_z = q_y \ (F_{02}) \\
C_xC_yS_z - S_xS_yC_z = q_z \ (F_{03})
$$

这里 $q = (q_r, q_x, q_y, q_z)$ 已知，且已做过归一化（这个条件在后面并没有用到），求解 $\theta_x, \theta_y, \theta_z$。

## 计算过程

平方相加得：

$$
C_y^2 C_z^2 + S_y^2 S_z^2 = q_r^2 + q_x^2 \ (F_{11}: F_{00}^2 + F_{01}^2) \\ 
C_x^2 C_z^2 + 4C_xC_yC_zS_xS_yS_z + S_x^2 S_z^2 = q_r^2 + q_y^2 \ (F_{12}: F_{00}^2 + F_{02}^2) \\ 
C_x^2 C_y^2 + S_x^2 S_y^2 = q_r^2 + q_z^2 \ (F_{13}: F_{00}^2 + F_{03}^2)
$$

用二倍角公式进行化简，得：

$$
\cos \theta_y \cos \theta_z = 2(q_r^2+q_x^2)-1 = A \ (F_{21}) \\
\cos \theta_x \cos \theta_z + \sin \theta_x \sin \theta_y \sin \theta_z = 2(q_r^2+q_y^2)-1 = B \ (F_{22}) \\
\cos \theta_x \cos \theta_y = 2(q_r^2+q_z^2)-1 = C \ (F_{23})
$$

如果 $\cos \theta_y \neq 0$：

$$
\cos \theta_x = \frac{C}{\cos \theta_y} \ (\text{from}\ F_{23}) \\
\cos \theta_z = \frac{A}{\cos \theta_y} \ (\text{from}\ F_{21})
$$

代入 $F_{22}$，并记 $M = \cos^2 \theta_y \in (0,1]$：

$$
\frac{AC}{M} + \sqrt{1-\frac{C^2}{M}} \sqrt{1-M} \sqrt{1-\frac{C^2}{M}} = B
$$

两边同时乘 $M$，将 $AC$ 移到右侧，两边平方，得：

$$
(M-C^2)(1-M)(M-A^2)=(BM-AC)^2
$$

## sympy 数值计算

可以看到，$A,B,C$ 为已知常数，这是一个一元三次方程，可以直接使用求根公式。这里只为获得数值解，使用 [sympy](https://docs.sympy.org/latest/index.html) 求根：

```py
import sympy
import math

qr, qx, qy, qz = (0.40642965, -0.42406866, -0.431619, 0.68460625)

A = 2 * (qr**2 + qx**2) - 1
B = 2 * (qr**2 + qy**2) - 1
C = 2 * (qr**2 + qz**2) - 1

M = sympy.symbols("M")

f = sympy.Eq((M - C**2) * (1 - M) * (M - A**2), (B * M - A * C) ** 2)
m_array = sympy.roots(f, M)
print(f"{m_array=}")
# m_array={0.132334460206920: 1, 0.947194427937568: 1, 0: 1}
```

得到 $M$ 之后，$\cos \theta_y = ±\sqrt{M}$；$\theta_y = \cos^{-1}(±\sqrt{M})$。注意 Python 中 `math.acos()` 的返回值在 $[0, \pi)$；从旋转的原理上来说，$\theta_x, \theta_y, \theta_z \in (-\pi, \pi]$，所以这里再取角度的负值。因为 x y z 都存在这样的情况，所以共有八种可能性。使用一个数组将所有可能的结果保存起来：

```py
posible_answers = []

for m in m_array:
    if m > 0 and m <= 1:
        for i in range(2):
            costy = (-1) ** i * math.sqrt(m)
            costx = C / costy
            costz = A / costy
            ty = math.acos(costy)
            tx = math.acos(costx)
            tz = math.acos(costz)
            posible_answers += [
                (tx, ty, tz),
                (-tx, ty, tz),
                (tx, -ty, tz),
                (tx, ty, -tz),
                (-tx, -ty, tz),
                (-tx, ty, -tz),
                (tx, -ty, -tz),
                (-tx, -ty, -tz),
            ]
```

接下来去验证所有的结果即可，注意要使用最开始的式子：

```py
def check(answer: tuple) -> bool:
    tx, ty, tz = answer
    Q = sympy.algebras.quaternion.Quaternion(qr, qx, qy, qz)
    Qx = sympy.algebras.quaternion.Quaternion(
        sympy.cos(tx / 2), sympy.sin(tx / 2), 0, 0
    )
    Qy = sympy.algebras.quaternion.Quaternion(
        sympy.cos(ty / 2), 0, sympy.sin(ty / 2), 0
    )
    Qz = sympy.algebras.quaternion.Quaternion(
        sympy.cos(tz / 2), 0, 0, sympy.sin(tz / 2)
    )
    QzQyQx: sympy.algebras.quaternion.Quaternion = sympy.simplify(Qz * Qy * Qx)
    sub: sympy.algebras.quaternion.Quaternion = QzQyQx - Q
    if sub.norm() < 0.001:
        return True


answers = []
for tx, ty, tz in posible_answers:
    if check((tx, ty, tz)):
        answers += [(tx, ty, tz)]
print(f"{answers=}")
# answers=[(-1.2920989064508213, 0.23186666079959756, 1.894926461258123)]
```

于是得到了结果。

## 边界情况

那么，如果 $\cos \theta_y = 0$ 呢？给定数据 `quaterion=(0.9780198, -0.19049281, -0.05851993, -0.06136183)`，计算得到 `costy=1.510758708743239e-08`, `C=0.9205759050431686`, `costx=60934674.72439538`，可以看到 $\cos \theta_y$ 的值非常接近 0，进而得到的 $\cos \theta_x$ 超过了 arccos 的定义域范围，会报错 `ValueError: math domain error`。

当 $\cos \theta_y = 0$ 时，$\theta_y = \frac{1}{2}\pi, \frac{3}{2}\pi, \frac{5}{2}\pi, \frac{7}{2}\pi$。对于上面每一组数据，代入 $\cos \theta_y = 0$ 之后得到的永远是不等式，很神奇。这说明这一组数据没有办法被表示为欧拉角的形式，所谓的万向节锁死问题。

这时我们可以令 $\theta_x = 0$，解出剩下两个角度：

$$
\cos(\theta_y/2) \cos(\theta_z/2)= q_r \\
- \sin(\theta_y/2) \sin(\theta_z/2) = q_x \\
\sin(\theta_y/2) \cos(\theta_z/2)= q_y \\
\cos(\theta_y/2) \sin(\theta_z/2)= q_z
$$

有

$$
\cos(\theta_y/2) = \pm \sqrt{q_r^2 + q_z^2} \\
\cos(\theta_z/2) = \pm \sqrt{q_r^2 + q_y^2}
$$

这里两个角都会解出四种情况，还是直接用 Python 来做判断。



## References

- [知乎｜鸡哥｜三维旋转：欧拉角、四元数、旋转矩阵、轴角之间的转换](https://zhuanlan.zhihu.com/p/45404840)
- [知乎｜杨智为｜四元数——基本概念](https://zhuanlan.zhihu.com/p/27471300)
- [知乎｜杨智为｜四元数——旋转](https://zhuanlan.zhihu.com/p/27541307)
- [知乎｜四元数(Quaternions)](https://www.zhihu.com/tardis/bd/art/97186723)
- Meurer A, Smith CP, Paprocki M, Čertík O, Kirpichev SB, Rocklin M, Kumar A, Ivanov S, Moore JK, Singh S, Rathnayake T, Vig S, Granger BE, Muller RP, Bonazzi F, Gupta H, Vats S, Johansson F, Pedregosa F, Curry MJ, Terrel AR, Roučka Š, Saboo A, Fernando I, Kulal S, Cimrman R, Scopatz A. (2017) SymPy: symbolic computing in Python. *PeerJ Computer Science* 3:e103 https://doi.org/10.7717/peerj-cs.103
- [sympy Documentation｜Find the Roots of a Polynomial Algebraically or Numerically](https://docs.sympy.org/latest/guides/solving/find-roots-polynomial.html)
- https://xie.infoq.cn/article/03d50d73ab19a5fc4d02d8a33
- https://www.zhihu.com/question/47736315/answer/236284413
