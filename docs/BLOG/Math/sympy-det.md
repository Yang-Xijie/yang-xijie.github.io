# sympy 库计算矩阵行列式

> 220502

## 线性代数背景

计算行列式的特征值是一件很简单的事情，直接用定义都可以计算：

$M_{ij}$ 是 $A$ 划去第 $i$ 行第 $j$ 列得到的 $n-1$ 阶矩阵 

余子式: $\det M_{ij}$

代数余子式: $C_{ij}=(-1)^{i+j}\det M_{ij}$

**行列式展开定理**

$$
\det A=|{a_{ij}}|_ {n\times n}=a_ {i1}C_ {i1}+a_{i2}C_{i2}+\cdots+a_{in}C_{in},\forall i,j=1,\cdots,n
$$

这样计算的方式中只有乘法和加法

## sympy计算

使用Python第三方库计算当然也是最简单不过的啦

```py
from sympy import *

M = Matrix([[1, 0, 0], [0, 1, 2], [0, 3, 4]])
print(M.det()) # -2
```

当然我们也可以定义一些符号来做符号运算

```py
from sympy import *

a, b, c, d = symbols("a,b,c,d")
M = [[1, 0, 0], [0, a, b], [0, c, d]]
print(Matrix(M).det())  # a*d - b*c
```

### 出现的问题

下面是我在固体物理课程中计算能带时列出的式子：

```py
>>> print(M) 
[[3.23e-17 - E, 2.50e-20, 1.06e-20], 
[2.50e-20, 3.18e-20 - E, 2.50e-20],
[1.00e-20, 2.50e-20, 3.23e-17 - E]]
>>> eq = Matrix(M).det()
-E**3 + 6.47e-17*E**2 - 1.04e-33*E + 3.32e-53
```

可以看到，这是三阶的情况，计算的行列式无误。但是当达到四阶的时候，意想不到的事情发生了

```py
>>> print(M) 
[[3.23e-17 - E, 2.50e-20, 1.06e-20, 0], 
[2.50e-20, 3.18e-20 - E, 2.50e-20, 1.06e-20],
[1.06e-20, 2.50e-20, 3.23e-17 - E, 2.50e-20],
[0, 1.06e-20, 2.50e-20, 1.29e-16 - E]]
>>> eq = Matrix(M).det()
(1.00*E**8 - 2.91e-16*E**7 + 3.13e-32*E**6 - 1.69e-48*E**5 + 4.92e-65*E**4 - 7.45e-82*E**3 + 4.61e-99*E**2 - 2.91e-118*E + 4.62e-138)/(1.0*E**4 - 9.70e-17*E**3 + 3.14e-33*E**2 - 3.39e-50*E + 1.07e-69)
```

你可以看到，当M为四阶的时候，M的结构和三阶时是一样的，可是行列式算出来却有分母？直接展开来思考，肯定是一个四阶多项式啊。虽然次数好像没问题，但这让人匪夷所思。

在我的计算过程中，计算好行列式之后下面需要令行列式等于0解出E：对于三阶的情况，这就是一个三阶多项式；但是对于四阶的情况，这可能直接变成了八阶多项式……我实际计算的是五阶的情况，甚至出了十七阶多项式。

### 调查

上SO搜了一下，也有人出现过相似的问题，主题是`关于sympy计算符号行列式`

[Speeding up computation of symbolic determinant in SymPy](https://stackoverflow.com/questions/37026935/speeding-up-computation-of-symbolic-determinant-in-sympy)

在这篇问答中，有人提到

> It looks like Matrix.det is calling a simplification function. For matrices 3x3 and smaller, the determinant formula is written out explicitly, but for larger matrices, it is computed using the **Bareis algorithm**. -- https://stackoverflow.com/a/37056325/14298786

简单来说 就是smypy对于高阶符号运算使用 [Bareis算法](https://en.wikipedia.org/wiki/Bareiss_algorithm) 这个算法中用到了除法。

为什么要用呢？复杂度低呗（详见[Bareis算法](https://en.wikipedia.org/wiki/Bareiss_algorithm)）。当然是好事情 但是对我来说就是大麻烦。

### 解决方案

查看[sympy文档](https://docs.sympy.org/latest/modules/matrices/matrices.html#sympy.matrices.matrices.MatrixDeterminant.det)

```
(method) det: (method: str = "bareiss", iszerofunc: Any | None = None) -> Any

method:
If it is set to 'bareiss', Bareiss’ fraction-free algorithm will be used.
If it is set to 'berkowitz', Berkowitz’ algorithm will be used.
Otherwise, if it is set to 'lu', LU decomposition will be used.
```

换[Samuelson–Berkowitz算法](https://en.wikipedia.org/wiki/Samuelson–Berkowitz_algorithm)试一下：

> ..., it performs no divisions, so may be applied to a wider range of algebraic structures.

```py
>>> print(M)
[[3.23e-17 - E, 2.50e-20, 1.06e-20, 0], 
[2.50e-20, 3.18e-20 - E, 2.50e-20, 1.06e-20],
[1.06e-20, 2.50e-20, 3.23e-17 - E, 2.50e-20],
[0, 1.06e-20, 2.50e-20, 1.29e-16 - E]]
>>> eq = Matrix(M).det(method='berkowitz')
1.0*E**4 - 1.93e-16*E**3 + 9.41e-33*E**2 - 1.35e-49*E + 4.29e-69
```

好了，这样问题就解决了，省去了我手写四阶展开式的时间。
