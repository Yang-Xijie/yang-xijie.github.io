# numpy 方法速查表

> 非本人总结……

||作用|
|-|-|
|1|**基本属性**
|`a.dtype`|数组元素类型 `float32,uint8,...`
|`a.shape`|数组形状 `(m,n,o,...)`
|`a.size`|数组元素数
|`a.itemsize`|每个元素占字节数
|`a.nbytes`|所有元素占的字节
|`a.ndim`|数组维度
|2|**形状相关**
|`a.flat`|所有元素的迭代器
|`a.flatten()`|返回一个1维数组的复制
|`a.ravel()`|返回一个1维数组，高效
|`a.resize(new_size)`|改变形状
|`a.swapaxes(axis1, axis2)`|交换两个维度的位置
|`a.transpose(*axex)`|交换所有维度的位置
|`a.T`|转置，`a.transpose()`
|`a.squeeze()`| 去除所有长度为1的维度
|3|**填充复制**
|`a.copy()`| 返回数组的一个复制
|`a.fill(value)`| 将数组的元组设置为特定值
|4|**转化**
|`a.tolist()`|将数组转化为列表
|`a.tobytes()`|转换为字符串
|`a.astype(dtype)`|转化为指定类型
|`a.byteswap(False)`|转换大小字节序
|`a.view(type_or_dtype)`|生成一个使用相同内存，但使用不同的表示方法的数组
|5|**复数**
|`a.imag`|虚部
|`a.real`|实部
|`a.conjugate()`|复共轭
|`a.conj()`|复共轭（缩写）
|6|**保存**
|`a.dump(file)`|将二进制数据存在file中
|`a.dump()`|将二进制数据表示成字符串
|`a.tofile(fid, sep="",format="%s")`|格式化ASCⅡ码写入文件
|7|**查找排序**
|`a.nonzero()`|返回所有非零元素的索引
|`a.sort(axis=-1)`|沿某个轴排序
|`a.argsort(axis=-1)`|沿某个轴，返回按排序的索引
|`a.searchsorted(b)`|返回将b中元素插入a后能保持有序的索引值
|8|**元素数学操作**
|`a.clip(low, high)`|将数值限制在一定范围内
|`a.round(decimals=0)`|近似到指定精度
|`a.cumsum(axis=None)`|累加和
|`a.cumprod(axis=None)`|累乘积
|9|**约简操作**
|`a.sum(axis=None)`|求和
|`a.prod(axis=None)`|求积
|`a.min(axis=None)`|最小值
|`a.max(axis=None)`|最大值
|`a.argmin(axis=None)`|最小值索引
|`a.argmax(axis=None)`|最大值索引
|`a.ptp(axis=None)`|最大值减最小值
|`a.mean(axis=None)`|平均值
|`a.std(axis=None)`|标准差
|`a.var(axis=None)`|方差
|`a.any(axis=None)`|只要有一个不为0，返回真，逻辑或
|`a.all(axis=None)`|所有都不为0，返回真，逻辑与
