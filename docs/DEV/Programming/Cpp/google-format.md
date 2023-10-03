# C++ 笔记 | Google C++ 风格指南学习 命名约定

> 摘自：[Google开源项目风格 | C++风格指南 7.命名约定](https://zh-google-styleguide.readthedocs.io/en/latest/contents/)
> 
> 选择分类的时候参考了[CSDN | 关于博客中转载和原创的文章 by JeffreyLau7](https://blog.csdn.net/jeffreylau7/article/details/51276136 "csdn.net")
> 
> 整理时间：200414
> 
> 注：只整理了作为一个C++初学者能看懂的部分

## 7.命名约定

### 7.1 通用命名规则

使用描述性的命名，让代码易于新读者理解

不要使用含糊不清的缩写

一些特定的广为人知的缩写是允许的, 例如用`i`表示迭代变量和用`T`表示模板参数

模板参数的命名应当遵循对应的分类: 类型模板参数应当遵循`类型命名`的规则, 而非类型模板应当遵循`变量命名`的规则

### 7.2 文件命名

文件名要全部小写, 可以包含下划线`_`, 如`my_useful_class.cc`

C++ 文件要以`.cc`结尾, 头文件以`.h`结尾. 专门插入文本的文件则以`.inc`结尾

不要使用已经存在于`/usr/include`下的文件名 (即编译器搜索系统头文件的路径), 如`db.h`

通常应尽量让文件名更加明确

定义类时文件名一般成对出现

内联函数必须放在`.h`文件中. 如果内联函数比较短, 就直接放在`.h`中

### 7.3 类型命名

所有类型命名——类, 结构体, 类型定义 (typedef), 枚举, 类型模板参数——均使用相同约定, 即以大写字母开始, 每个单词首字母均大写, 不包含下划线. 

如 `MyExcitingClass` `MyExcitingEnum`

### 7.4 变量命名

变量 (包括函数参数)、数据成员名、结构体成员变量名一律小写, 单词之间用下划线连接. 

如`a_local_variable` `a_struct_data_member`

类的成员变量以下划线结尾 如`a_class_data_member_`

译者(acgtyrant):

感觉 Google 的命名约定很高明, 比如写了简单的类`QueryResult`, 接着又可以直接定义一个变量`query_result`, 区分度很好;

再次, 类内变量以下划线结尾, 那么就可以直接传入同名的形参, 比如`TextQuery::TextQuery(std::string word) : word_(word) {}`, 其中`word_`自然是类内私有成员.

### 7.5 常量命名

声明为`constexpr`或`const`的变量, 或在程序运行期间其值始终保持不变的, 命名时以`k`开头, 大小写混合

如`const int kDaysInAWeek = 7;`

所有具有静态存储类型的变量 (例如静态变量或全局变量) 都应当以此方式命名

### 7.6 函数命名

常规函数使用大小写混合, 我选择`MyExcitingFunction()` `MyExcitingMethod()` `AddTableEntry()` `DeleteUrl()`

对于首字母缩写的单词, 更倾向于将它们视作一个单词进行首字母大写

例如, 写作 `StartRpc()` 而非 `StartRPC()`

取值和设值函数的命名与变量一致. 一般来说它们的名称与实际的成员变量对应. 例如 `int count()` 与 `void set_count(int count)`

### 7.8 枚举命名
新代码应该尽可能优先使用常量风格

枚举的命名应当和常量一致, 如 `kEnumName`

如:

```cpp
enum UrlTableErrors {
  kOK = 0,
  kErrorOutOfMemory,
  kErrorMalformedInput,
};
```

### 7.9 宏命名

不推荐使用宏, 一定要用, 像这样命名: `MY_MACRO_THAT_SCARES_SMALL_CHILDREN`
