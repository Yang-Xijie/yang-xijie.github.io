# 面向开发的 Markdown 讲座

> [Bilibili视频教程](https://www.bilibili.com/video/BV1jV411j7mz)

**说明**：所讲的内容包括但不限于：使用`markdown`的原因、`markdown`基础语法、对`markdown`中路径和互联网资源的理解、`markdown`编写工具、导出、发布……

**面向对象**：需要进行合作编程开发的同学（主要）；没有使用过`markdown`风格写过文字的同学。教程以使用`macOS`的同学为主。

**Lecture特色**：不仅仅讲`markdown`本身，会从`markdown`延伸出去，有一些扩展的内容

## 表达与说明的方式
我们要给别人说明一样东西、一样事情的时候，往往需要至少一种的表达方式：比如用语言、用文字、用图片、视频、音乐等媒体；或者将它们结合起来，比如`PPT`。

但其实一般来说，更方便的保留和传播的一种方式是文字。但如果只有文字，总是会让人觉得有些索然无味。这时，带格式的文字作为一种增强的表达方式出现了。大家最常用的可能就是`Microsoft Word`。你在`Word`中敲好文字，然后添加一些格式，比如加粗、斜体、居中、设置段落格式、艺术字和颜色调整；这样文字也变得有表现力了起来。

但是，对于从事开发的开发者们来说，`Word`并不够高效。虽然它提供的格式能够增强文本的表现力，但这些格式很难添加和管理——至少，你得有`Word`这款付费的软件才能看到、添加、修改这些格式。另外，`Word`提供的格式太多了，对于开发者来说，我们需要一些格式来增强文字的表现力，但是可能并不需要太多的格式（比如我们希望某种格式能加粗我们软件说明书中的重要部分，能够有层级结构让我们的说明结构清晰便于浏览；但是我们不需要什么论文管理的功能，也不需要什么艺术字，颜色什么的也不太需要……）

再具体的来说，`Word`的文件是二进制文件，它的后缀一般是`.doc`或者`.docx`：这个文件在机器中的本质是一长串的`0`和`1`，里面不仅存储了你写的文字，也存放了这些文字的样式；而这一些`0`和`1`**只有用专门的软件**`Word`才能打开（这其中可能需要解压、按照特定顺序读取等步骤）。

与这种二进制文件相对的呢，是纯文本文件，也就是我们常见的后缀为`.txt`的文件。这一类文件呢，里面从开始到结束，存储的就是一个个字符：比如我在`hello.txt`里面写入

```
Hello, world!
你好，世界！
```

那么，这个txt文件其中的内容就是`H`后面跟上`e`再跟上…再跟上一个英文`!`再跟上一个换行符`\n`…再跟上一个中文`！`最后跟上一个文件结束符`EOF`（End of File）。而这些字符都是可以由计算机系统直接读取并且显示出来的，（当然了，本质上这些符号在计算机内还是以`0～1`的形式存储的），因此读取要比`Word`方便（不需要特定的软件）、读取速度要比`Word`快得多；由于其中不带格式，大小也要比`Word`文档小得多。

### Markdown引言

刚刚我们说了文字是很常见的一种表达方式，用`txt`文件就可以在计算机中方便的呈现文字；我们也说了格式是可以增强文本的表现力的，比如用`Word`给这些文字添加格式。但问题是单单`txt`的表现能力捉急，`Word`中添加格式的操作成本、存储成本都太高了（后面讲`Git`还会说，由于`.docx`文件是二进制文件，其无法用`Git`进行逐行管理），能不能找到二者的平衡呢？

有，这个东西就是`Markdown`。

`Markdown`其实是一种写作风格/方式，我们用这种风格/方式写出来的**纯文本文件**（和`.txt`是一样的）叫做**markdown文件**，一般以`.md`作为文件后缀（而不是`.txt`）。`.md`文件虽然是纯文本，但其中用一些特殊的字符（如`* # [] () …`）给纯文本带来格式（这与`html`文件是相似的，也可以将`markdown`看作是简单的`html`）。这些格式通过某种方式进行渲染（注：渲染：指将计算机中的某些数据呈现在屏幕上）你就可以看到它们代表的格式了！

#### Markdown举例

说了这么多，我们还没看到过`markdown`文件呢，来看几个例子吧：

〇 （刚刚说到）开发者在写软件说明书的时候会用到`markdown`：

几乎每个`GitHub`仓库都有一个`markdown`文件`README.md`用来对项目做一个简单的说明。（肯定有同学不知道`GitHub`是什么，我们暂时把它理解为一些开发者存放他们写好的代码的地方）

[GitHub｜SwiftFormat](https://github.com/nicklockwood/SwiftFormat)
* `Xcode`的小插件：用来格式化Swift代码
* 其中的`README.md`就是用`markdown`文件，通过`GitHub`的网页将其渲染呈现在你面前。

〇 （为了提高写作效率（有时添加格式蛮麻烦的））写作者有的时候也会用这种风格：

[GitHub｜git flight rules](https://github.com/k88hudson/git-flight-rules)

[GitHub｜How To Ask Questions The Smart Way](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way)

我的这篇讲稿也是用`markdown`写的（事实上我现在手上的几乎所有文字都是用`markdown`来写的）

国内的博客网站：`CSDN`和`简书`都支持`markdown`格式；用`markdown`来做学习笔记是很方便的。

〇 代码注释：

比如`Xcode`支持的`markup`注释风格（类似，换了个名字hh）

[CSDN｜Swift Markup Formatting Syntax](https://blog.csdn.net/qq_45379253/article/details/113253433)

### Markdown语法
下面我们来介绍`markdown`文件到底怎么写：

说“语法”什么的有点专业了。刚刚我们说到——`markdown`用一些特殊的字符（如`* # [] () …`）给纯文本带来格式，其实语法指的就是这些规则。那么下面我们就来学习如何用这些特殊符号来在纯文本中表达格式。

#### 具体语法
[GitHub Guides | Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

`markdown`有不少扩展的语法，我们主要学习它最基础的语法，和一些`GitHub`支持的语法，因为我们之后写`markdown`文件可能主要是用来写项目的`README.md`，而这些项目的代码仓库，我们很可能就在`GitHub`存放。

##### Headers 标题
`1`～`6`个井号加一个空格再加上标题的名称

```
## 一级标题
### 二级标题
……
###### 六级标题
```

有的同学可能会问，那七级标题呢？嗯，是没有的。事实上，五级标题和六级标题都很少会用到，这些绝对够用了

##### Emphasis 加粗和斜体
```
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_
```

*This text will be italic*

_This will also be italic_

**This text will be bold**

__This will also be bold__

_You **can** combine them_

一般我们单个使用的时候用`*`多一些，但是两种格式组合使用的时候就随意了。

##### Lists 列表

###### Unordered 无序列表

这里可以缩进的哦

```
* Item 1
* Item 2
    * Item 2a
    * Item 2b
```

* Item 1
* Item 2
    * Item 2a
    * Item 2b

###### Ordered 有序列表
这里可以缩进的哦，缩进会重新编号，或者变成小标题（如`1.1` `2.1.3`这样）

```
1. Item 1
1. Item 2
1. Item 3
    1. Item 3a
    1. Item 3b
```

1. Item 1
2. Item 2
3. Item 3
    1. Item 3a
    2. Item 3b

###### Task Lists 任务列表

```
- [x] this is a complete item
- [ ] this is an incomplete item
```

- [x] this is a complete item
- [ ] this is an incomplete item

##### Links 链接

`[Text](url)`：中括号，后面小括号。小括号里面放链接，中括号里面放说明（必须）；不需要说明的话，可以直接写链接

直接写链接会直接被转换为可以点击的链接；也可以在两侧加上`<`和`>`

```
[GitHub Official Site](https://github.com)

https://github.com
<https://github.com>
```

[GitHub Official Site](https://github.com)

https://github.com

<https://github.com>

##### Images 图片

`![Text](url)`：感叹号，中括号，小括号。小括号里面放图片链接，中括号里面放图片说明（不必须；写了的话会在图片下方或某处显示说明，当因为某种原因图片无法加载的时候，显示时也会用说明替代图片）

```
![GitHub Logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)
```

![GitHub Logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)

关于链接我们之后会详细来说。

##### Inline Code 行内代码

```
`Swift`中，`var`定义变量，`let`定义常量
```

`Swift`中，`var`定义变量，`let`定义常量

##### Code Block 代码块

用一对三个反撇\`\`\`包裹，在最开始三个反撇后可以加代码的语言名称或简写以在渲染时获得高亮支持。

\`\`\`swift

var natural_numbers: Array<Int> = [0,1,2,3]

print(natural_numbers.capacity)

\`\`\`

```swift
var natural_numbers: Array<Int> = [0,1,2,3]

print(natural_numbers.capacity)
```

一般支持的代码高亮会有很多，比如：`shell`、`bash`、`c`、`cpp`、`java`、`objectivec`、`python`、`swift`、`yaml`、`html`、`xml`等

##### Blockquotes 引用

```
As Tim Cook said:

> Fearlessness means taking the frst step, 
> even if you don't know where it will take you.
```

As Tim Cook said:

> Fearlessness means taking the frst step, 
> even if you don't know where it will take you.
> 
> ——Tim Cook's Commencement Address at Duke University, 2018

我一般会用它来在文章开头写一下文档的更新日期和作者。

##### Tables 表格

You can create tables by assembling a list of words and dividing them with hyphens `-` (for the first row), and then separating each column with a pipe `|`:

```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

#### 其他GitHub支持的语法

更多`Github`支持的`markdown`语法可以查看[GitHub Guides | Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

#### 对文件路径的理解

我们在插入链接的时候，会使用：

```
[Google](https://www.google.com) is your best friend!
```

[Google](https://www.google.com) is your best friend!

方括号里面放你要呈现的名字，圆括号里面放网页的链接。

更普通的，这个链接还可以换成文件：

```
点击查看[帮助文档](./doc/help.md)
```

这个路径是相对路径，表示和当前的md文件在同一个路径下的`doc`文件夹里面的`help.md`文件，一般我们都会将md文件放在一个总的文件夹中，这样它们之间就可以使用相对路径相互引用了。

如果是在自己电脑上写md，也可以写绝对路径。但是这样一旦那个文件移动位置，使用绝对路径就找不见那个文件了。使用相对路径的话，由于一般md文件会随着总文件夹跟着其他的文件一起走，所以一般不会出现找不到的问题。

更普通的，还可以换成当前文档中的某个大标题：

```
点击跳转到这篇markdown的[Intro部分](#intro)
```

#### 对url资源的理解

在我们插入图片的时候，我们使用了这样的语法：

```
![图片名称](图片链接)
```

本质上来说，你获取一张网络上的图片，是在服务器（24h不关机的电脑）的文件系统里面获取了这张图片。但为了能保证一张图有一个唯一的标志，一般一张图都会有一个自己的链接。

打开带图片的网站，右键图片，就可以看到`复制图片链接`的按钮从而获取图片的链接。

这里的`图片链接`也可以是刚刚的相对路径，比如：

```
![Markdown图标](./media/markdown_icon.png)
```

但这样，你就需要在和你现在写的`markdown`的同一目录下，放一个`media`文件夹，里面有这张`markdown_icon.png`的图片。

有的时候，图片和代码相比起来，是个庞然大物（`1KB` vs `1MB`），这时我们不希望将图片加入到项目中（指不希望项目的体积很大，别人从`GitHub`上下载项目时花的时间过久），可是在项目说明中还需要加入图片进行说明，这时怎么办呢？最简单的，将图片压缩一下（`1MB->100KB`）扔进项目文件夹，这是最省心的…但要是图比较多，一般来说，我们会选择某些厂商的对象存储服务，将这些图片资源放到比如阿里云的服务器上，然后这个服务把图片的网络链接给你，你就可以在`markdown`中使用这个链接了。如果没有那么正式，那么这种服务叫做图床。比如我一直在用的[聚合图床](https://www.superbed.cn)，你把图片丢进去，它帮你将图片转为一个链接。但是使用这种服务也有需要注意的地方，如果运营图床的工作室哪天跑路了，你放进去的图片可能就没了。

#### 添加目录

不少平台都支持使用`[toc]`来添加目录。你只需要输入`[toc]`，平台就会帮你自动渲染生成目录。

但也有一些平台不支持这样，这时你需要使用VS Code中的`Markdown All in One`插件，使用这个插件提供的`自动生成目录`功能来添加目录。

#### 其他一些注意事项

有的时候你在`markdown`明明换行了，可是上传到`GitHub`上面一看，文字都粘在一起了。这是为什么呢？

英文在分段的时候，不像我们写文章段前空两格，他们会直接在两段之间多空一行。一般的回车只是用来方便阅读，不然一行的内容太长了。

如果你不希望这种方式生效，可以在一行后面加两个空格；但这样很麻烦，还是多加回车吧；最好在每种语法前后都空行，这样也能有效减少语法不被识别的情况

（注：多于2个的连续回车markdown会将它们当作一个回车哦）

### Markdown工具介绍

#### macOS

##### Typora

[Typora官网](https://www.typora.io)

所见即所得的`markdown`编辑软件，全平台；各种意义上都应该是`markdown`编辑的首选！

主要用来写单独的markdown（比如我今天要写讲稿了，用markdown写的话我就会考虑Typora）；也可以开一个文件夹专门放自己的笔记……

##### VS Code

安装插件`Markdown All in One`，会支持不少快捷操作。

`VS Code`作为程序员中口碑最好的编辑器，写写`markdown`什么的肯定没问题！拖入一个文件夹新建`markdown文件`就可以编辑了！

一般来说，软件开发的项目中，代码都是和`markdown文件`在一起的，以后如果有一些需要在`VS Code`打开的项目，使用`VS Code`编写`README.md`或者其他的`markdown文件`也是很方便的一个选择。

##### Xcode

在`Xcode`中也可以和添加`代码文件`一样添加`markdown文件`。

##### 其他

如果你在听了这次lecture之后，打算和我一样以后自己的文稿都用`markdown`来写，那我觉得你可以考虑一些功能更强大的软件。这些软件基本都是付费的，在`App Store`搜索`markdown`就有很多；有些是买断制的，有些是订阅制的；都各自有一些独特的功能，比如发布服务、自动备份、图片上传等等，感兴趣的同学也可以看看知乎等平台的安利文章，自己下载试用版试用。

#### 网络平台

`CSDN`和`简书`支持`Markdown`写作。

- `CSDN`对各种语法支持的比较好；`简书`只支持比较基础的`Markdown`语法。
- `CSDN`的主要文章都是技术文章；`简书`可能偏杂文多一些，但也有不少质量很高的技术文章。大家以后自己的学习经历、开发笔记也都可以上传到这些平台让更多人看到。

### 关于不同风格和扩展的说明

如果我们只是写简单的`Markdown`文稿，上面的这些语法已经完全够用了。

不过既然能用符号表示格式，那么能不能添加更多的语法进来呢？当然可以，比如在`markdown`里面使用`$y=x^2$`表示这是一个`LaTeX`公式（怎么敲`LaTeX`可以查看我之前整理的[LaTeX整理 | 简易符号 Markdown公式编辑](https://blog.csdn.net/qq_45379253/article/details/105368552)），如果渲染`markdown`的软件支持，那么它就会被显示为$y=x^2$；比如说很多编辑器都支持`[toc]`表示插入全文目录（但可惜的是`GitHub`不支持，一般会用`VS Code`的插件来创建目录）；前面我们讲了表格，语法更多的`markdown`还可以以某种方式设定表格每列的对齐方式；由于`markdown`最终会被渲染为网页（`html文件`），因此你在其中加入`html标签`也是可以的。这些其他的格式大家都可以去`CSDN`搜索`markdown`教程找到，但是在使用的时候也要注意看自己的`markdown`编辑器是不是支持这些语法哦。

这个[CSDN｜Markdown语法学习](https://blog.csdn.net/qq_45379253/article/details/104876463)是我最开始学习`Markdown`整理的语法，里面就有介绍了很多其他的格式；但事实上我写了一年的`markdown`，有些根本就没用过……所以今天我也只讲了最基础的一些格式。

还有一点，反斜线还有行内代码可以用来输入可能会被当作`markdown`语法的符号。比如你想在markdown中输入一个星号`*`，可能你一不小心就发现星号被markdown渲染成了格式。这时你可以用行内代码包裹，\`\*\`，或者用反斜线`\*`，这样markdown就不会把这些符号当成格式了。

### Markdown的导出

有的时候（大多数时候）我们都需要将自己写的`markdown`发个别人看，这时当然我们希望别人看到的是带格式的，而不是纯文本文件。

如果我们在`GitHub`上上传了`README.md`，那么`GitHub`会帮我们自动把`.md`文件渲染为带格式的网页方便查看。在`CSDN`和`简书`等平台发布也是一样的。

不过如果是自己导出的话：

* 可以导出`xxx.md`，但这样对方的电脑上需要有`markdown`编辑软件打开才能看到格式，不过这样的话对方不仅可以查看，也能编辑；
* 如果只是让别人查看的话，一般我们会考虑导出`PDF文件`，也就是打印，然后选择保存PDF文件；
* 也可以直接导出为`图片`（一些软件支持）；
* 或者我们还可以导出为`网页`（html），这样对方需要用浏览器才能打开也有些麻烦…不过如果你是导出为网页再部署，那么对方通过链接就可以访问，这就变得很方便了

### Markdown的发布

下面的内容有些进阶也没那么重要。我讲这一块呢，是想告诉大家大家现在看到的这份讲稿和这个页面是怎么做出来的。一方面是想让大家了解`markdown文件`发布的过程，另一方面是希望大家学了Git、了解了GitHub之后也能一起修改现在网页上的这些讲稿。

感兴趣的同学可以认真听一下；因为我不会花很多时间在这上面，也希望其他同学听一听：

有的同学可能在学了`markdown`后就一直用它来写文章，写的多了就想把它发布出来，比如建一个个人网站，把这些文章放上去。然而`markdown`是纯文本的，所以要将带格式的网页发布出来，我们需要借助一些工具；这样的工具有很多，下面介绍一个：[mdbook](https://github.com/rust-lang/mdBook)

我们可以在`Mac`上安装`Homebrew`，然后在终端用命令行输入：

```shell
brew install mdbook
```

之后就可以使用它了！

`mdbook`可以方便的把**一系列md文件**组织成一个`book`，用来发布很多`markdown`文件的时候很容易。`mdbook`使用`SUMMARY.md`这个文件确定展示的边栏；`book.toml`这个文件来对它生成的网页做一些设置。

我们只需要在准备好md文件，编辑好`SUMMARY.md`和`book.toml`之后，确定自己电脑装好了`mdbook`，在和`book.toml`同级的文件夹下执行：

```shell
mdbook build
```

就可以得到一个`book`的文件夹，将这个文件夹上传到服务器，别人去访问就可以看到mdbook渲染好的页面了。

如何直接在自己的电脑上查看生成的网页的效果呢？在和`book.toml`同级的文件夹下执行：

```shell
mdbook server
```

那么如何将这个文件夹上传至`GitHub`呢？我们可以将刚刚得到的`book`文件夹上传至`GitHub`，然后开启`GitHub Pages`的服务。但更方便的是，直接把这个文件夹传上去，使用`GitHub Action`将这个文件夹在另一个`Git`分支生成网页，然后用`GitHub Pages`发布出去；这样做的好处是：每次修改上传，发布都是自动的，这样被人看到你的网页/讲稿就总是最新的。如果大家也想帮忙一起建设`THU iOS Club`的`Tutorial`，在学了`Git`之后就可以提`Pull Request`喽！

### 文字编辑效率up技巧

最后呢，再教大家一些快速写文档的方法。这种方法在macOS上的大多数文字/代码编辑软件上都适用（包括`Xcode`）。

〇 双击选中一个词：这里词指一个中文的词语或者一个英文的单词

〇 三击选中一行

〇 ⌥左右：以词为单位移动光标

〇 ⌘上下左右：移动光标到行首/行未/文头/文末

〇 按住⇧：文字选中；⇧上下左右 / ⇧⌥左右 / ⌘⇧上下左右

〇 按住⌥：矩形区域选中

〇 ⌥⌫、⌘⌫；fn⌫：删除词、删除到行首；向后删除 delete；⌘X也是一种删除的方式

## Homework

〇 （markdown语法：粗体/斜体）

用`markdown`写出带格式的文字：`Hello, world!`其中`Hello`用**粗体**，`world`用*斜体*。

〇 （markdown语法：表格）

用`markdown`语法列一个两行五列的表格：表头为**周一到周五**，表的内容为那天你的**早八课程**；如果某天没有早八课程，那么对应的格空下来不填写。

〇 （markdown图片插入）

在`markdown`中插入图片时小括号中可以填写图片在互联网上的（），也可以填写在文件管理器（如`访达`）中的**图片**与**markdown文件**的（）。

〇 （其他markdown语法）

阅览`Github`支持的`markdown`语法[GitHub Guides | Mastering Markdown](https://guides.github.com/features/mastering-markdown/)，使用删除线语法在右边的文字中只添加符号来表示“Google是你最好的朋友”）：`Baidu Google is your best friend.`（提示：`crossed out`）

### Answer

〇 （markdown语法：粗体/斜体）

用`markdown`写出带格式的文字：`Hello, world!`其中`Hello`用**粗体**，`world`用*斜体*。

```
**Hello**/__Hello__ 和 _word_/*world* 的任意组合
```

〇 （markdown语法：表格）

参考：

```
Monday | Tuesday | Wednesday | Thursday | Friday
- | - | - | - | -
 | | Technical Drawing | | Signal and System
```

〇 （markdown图片插入）

链接 相对路径

〇 （其他markdown语法）

```
~~Baidu~~ Google is your best friend.
```
