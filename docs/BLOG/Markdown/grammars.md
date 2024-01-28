# Markdown 语法学习 精简版

> <span id="top">**文章开头**</span>

点击[这里](#now)回到下方介绍 `页面跳转` 的阅读位置

点击[这里](#catalog)回到下方介绍 `toc` 的阅读位置

此笔记学习摘抄自[Markdown语法大全(超级版)](https://www.jianshu.com/p/ebe52d2d468f "jianshu.com")，并根据笔者的使用不断更新，基本使用应该足够。

## 最常用

### 分级标题

```
# 一级标题 (注意有空格)
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题  <!--最多6级标题-->
```

### 目录

在任意位置插入 `[toc]` 显示全文<span id="catalog">**目录**</span>结构

示例见文章开头（点击[这里](#top)跳转到开头查看目录）

### 斜体/粗体/删除线/下划线/背景高亮

```
*斜体*    _斜体_
**粗体**    __粗体__
***加粗斜体***    ___加粗斜体___
~~删除线~~
<u>下划线</u>
==背景高亮==
```

*斜体*    _斜体_

**粗体**    __粗体__

***加粗斜体***    ___加粗斜体___

~~删除线~~

<u>下划线</u>

==背景高亮==

### 无序列表/有序列表

#### 无序列表

```
* 无序列表项 一
+ 无序列表项 二
- 无序列表项 三
```

* 无序列表项 一
+ 无序列表项 二
- 无序列表项 三

#### 多级无序列表

```
* 今天`* + 空格键`
* 明天
    * 学习 `TAB(或4个空格) + * + 空格键`
	* 购物
	    * 面包
	    * 牛奶
* 后天
```

* 今天`* + 空格键`
* 明天
    * 学习 `TAB(或4个空格) + * + 空格键`
	* 购物
	    * 面包
	    * 牛奶
* 后天

#### 有序列表/多级有序列表

```
1. 有序列表项 一 `数字 + . + 空格键`
2. 有序列表项 二
    1. 有序列表项 二(1) `TAB(或4个空格) + 数字 + . + 空格键`
    2. 有序列表项 二(2)
        1. 有序列表项 二(2).1
3. 有序列表项 三
```

1. 有序列表项 一 `数字 + . + 空格键`
2. 有序列表项 二
    1. 有序列表项 二(1) `TAB(或4个空格) + 数字 + . + 空格键`
    2. 有序列表项 二(2)
        1. 有序列表项 二(2).1
3. 有序列表项 三

### 任务列表

```
- [ ] 任务一 未做任务 `- + 空格 + [ ]`
- [x] 任务二 已做任务 `- + 空格 + [x]`
```

- [ ] 任务一 未做任务 `- + 空格 + [ ]`
- [x] 任务二 已做任务 `- + 空格 + [x]`

### 表格

第一行为表头，第二行分隔表头和主体部分(如果表格无法显示可以尝试把第二行的 `-` 变为 `---` )，可以指定所在列的对齐方式，第三行开始每一行为一个表格行。列与列之间用 `|` 隔开。(注：原生方式的表格每一行的两边也要有 `|` )

**对齐方式** `:- 左对齐` `- 中心对齐` `-: 右对齐`

```
第一列|第二列|第三列
:-|-|-:
a11|a12|a13
a21|a22|a33
a31|a32|a33
```

|表头一|表头二|表头三
:-|-|-:
a11|a12|a13
a21|a22|a33
a31|a32|a33

### 超链接

[ ]里写链接文字，( )里写链接地址, ( )中的" "中可以为链接指定title属性，title属性可加可不加。title属性的效果是鼠标悬停在链接上会出现指定的 title文字，链接地址与title前有一个空格。

```
右边是链接[链接文字](链接 "title")
```

```
右边是链接[GitHub](https://github.com "GitHub")
```

右边是链接[GitHub](https://github.com "GitHub")

### 插入图片

**格式**：`!` `[图片标题]` `(图片地址 "图片Title”)`

其中`图片标题`会被某些网站和编辑器显示在图片下方

### 代码块

#### 行内代码块

用“ \` ”左右包裹代码

#### 多行代码块

用“ \`\`\` ”上下包裹代码，在第一个“ \`\`\` ”后添加语言名称获得不同的高亮效果

如：cpp，python，swift

### 对齐方式

```
<center>行中心对齐</center>
<p align="left">行左对齐</p>
<p align="right">行右对齐</p>
```

<center>行中心对齐</center>
<p align="left">行左对齐</p>
<p align="right">行右对齐</p>

### 分割线

```
* * *
***
- - -
---
```

* * *

***

- - -

---

### 换行

不同markdown编辑器可能有不同的换行方式，最简单为直接敲回车

markdown文本内的连续两个或多个回车会被替换为一个回车

## 高级

### 设置字体/颜色

```
<font face="宋体" color=blue size=5>蓝色的字～</font>
```

<font face="宋体" color=blue size=5>蓝色的字～</font>

#### 常用颜色

浏览器支持的所有颜色请跳转参考

[现代浏览器支持的140种已命名的颜色](https://htmlcolorcodes.com/zh/yanse-ming  "htmlcolorcodes.com")

常用颜色名称:
* 按网站顺序排列
* orange pink  gold yellow purple greenyellow lightgreen green aqua lightblue blue wheat brown white snow linen silver gray black

最常用|其他
-|-
<font color=red>red</font>|<font color=greenyellow>greenyellow</font>
<font color=orange>orange</font>|<font color=lightgreen>lightgreen</font>
<font color=yellow>yellow</font>|<font color=lightblue>lightblue</font>
<font color=green>green</font>|<font color=pink>pink</font>
<font color=aqua>aqua</font>|<font color=gold>gold</font>
<font color=blue>blue</font>|<font color=silver>silver</font>
<font color=purple>purple</font>|<font color=brown>brown</font>
||<font color=wheat>wheat</font>|
||<font color=linen>linen</font>|
||<font color=snow>snow</font>|
||<font color=gray>gray</font>|
||<font color=black>black</font>|

### 锚点

也就是 `跳转`

```
1. [点击这里跳转到第一段](#jump1)
2. [点击这里跳转到第二段](#jump2）

### <span id="jump1">第一段</span>

### <span id="jump2">第二段</span>
```

```
<span id="now">当前位置</span>
点击[这里](#top)跳转到开头
点击[这里](#bottom)跳转到结尾
```

<span id="now">**当前位置**</span>

点击[这里](#top)跳转到开头

点击[这里](#bottom)跳转到结尾

### 注脚

```
使用 Markdown[^1]可以效率的书写文档, 直接转换成 HTML[^2]。

[^1]: Markdown 是一种纯文本标记语言
[^2]: HyperText Markup Language 超文本标记语言
```

使用 Markdown[^1]可以效率的书写文档, 直接转换成 HTML[^2]。

点击[这里](#bottom)跳转到结尾查看<span id="footnote">**注脚**</span>的显示效果

[^1]: Markdown 是一种纯文本标记语言

[^2]: HyperText Markup Language 超文本标记语言

### 多级引用

```
>>> 请问 Markdwon 怎么用？ - 小白

>> 自己看教程！ - 愤青

> 教程在哪？ - 小白

`[^_^]: # 无法显示时记得空行`
```

不同编辑器的显示情况不同

>>> 请问 Markdwon 怎么用？ - 小白

>> 自己看教程！ - 愤青

> 教程在哪？ - 小白

### LaTeX公式

* 在数学公式的前后加`$`是行内公式

```
我们在初中数学课上已经对一次函数$y=x+a$有所了解。
```

我们在初中数学课上已经对一次函数$y=x+a$有所了解。

* 在数学公式的前后加`$$`是独占一行的公式
```
下面我们来认识一下二次函数$$y=ax^2+bx+c$$
```
下面我们来认识一下二次函数$$y=ax^2+bx+c$$

- - -

```
行内公式：$\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$
块级公式：
$$	x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$
$$ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } } $$
```

行内公式：$\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$

块级公式：

$$x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

$$\frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} = 1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}{1+\frac{e^{-8\pi}} {1+\ldots} } } }$$

## 其他

### 转义字符

通过在Markdown字符前使用\来忽略（或转义）Markdown格式。

Markdown允许您使用反斜杠转义来生成文字字符，否则这些字符在Markdown的格式化语法中具有特殊含义。 例如，如果您想用文字星号包围一个单词，则可以在星号之前使用反斜杠，如`\*literal asterisks\*`  \*literal asterisks\*

Markdown为以下字符提供反斜杠转义(但是CSDN不太支持)：

\\反斜杠 \`反引号 \*星号 \_下划线 \{\}大括号 \[\]中括号 \(\)小括号  \#井号 \+加号 \-减号 \.英文句号 \!英文感叹号

### 内联 HTML 语法/特殊字符自动转义

对于 Markdown 中未包含的标签, 可以直接使用 HTML标签，例如用 HTML `<a>` 标签替代 Markdown 的链接语法

在 HTML 中, 有一些字符需要特殊对待，如果你想将它们用作字面量, 则需要将它们转义为字符实体

特殊字符|代码
-|-
&amp;|`&amp;`
&lt;|`&lt;`
&gt;|`&gt;`
&quot;|`&quot;` `&#34;`
&apos;|`&apos;` `&#39;`

### 注释

```
<div style='display: none'>
注释
</div>
```

```
<!-- 注释 -->
```

```
[//]: # (哈哈我是最强注释1，不会在浏览器中显示。)
[^_^]: # (哈哈我是最萌注释2，不会在浏览器中显示。)
```

### 空格

```
【1】 &nbsp; 半角的不断行的空白格（推荐使用）
【2】 &ensp; 半角的空格
【3】 &emsp; 全角的空格
```

* 【1】 &nbsp; 半角的不断行的空白格（推荐使用）
* 【2】 &ensp; 半角的空格
* 【3】 &emsp; 全角的空格

---

> <span id="bottom">**文章结尾**</span>

点击[这里](#now)回到介绍 `页面跳转` 的阅读位置

点击[这里](#footnote)回到介绍 `注脚` 的阅读位置
