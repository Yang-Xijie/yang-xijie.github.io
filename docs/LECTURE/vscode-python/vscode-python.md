# 在macOS上用VSCode配置Python环境的一种思路

> 此篇文章较过时 推荐使用miniconda配置虚拟环境 使用vscode编写python带啊吗

> [Bilibili 视频版](https://www.bilibili.com/video/BV1Y5411E7yc)

本教程使用`Intel` `MacBook Pro`，搭载`macOS 11.1 Big Sur`录制。`Python3`版本`3.9.1`，`VS Code`版本`1.53.0`。

注：本教程不一定适用于`M1 Mac`。不一定适用于`10.14 (Mojave)`及以前的系统。

大家好，我是杨希杰。今天给大家带来的是用`macOS`在`VS Code`上写`python`的教程。注意，我的这份教程并不教你怎么写`python`代码，而是告诉你一种配置`python`环境的方式，让你用`VS Code`、舒舒服服的敲`python`。

啊，那为什么是**一种**方式呢？因为`python`的安装和包的管理有太多种方式了，每个人的电脑里随着使用`python`的数量也越来越多。我虽然对配置`python`环境也有一点自信，但是仅仅是对我日常使用的一种配置`python`环境的方式有自信。这种方式较为简单，我也想分享给大家。

话不多说，我们直接开始！

这份讲稿的链接在视频简介里，可以在我的个人网页查看。如果教程中有不妥或不正确的地方，也欢迎在评论区与我讨论。

## 安装必要工具

### 下载安装Command Line Tools

`Command Line Tools`是什么？如果你已经开始写了某种语言的代码，但是你还没有安装`Command Line Tools`，那我强烈推荐你安装。`Command Line Tools`是苹果推出的命令行工具，里面包含了很多东西——比如`C/C++`的编译器、调试器，比如`Swift`的语言包，当然应该也包括我们想要的的`python`。如果你之后要使用`MATLAB`，那么`MATLAB`也会依赖`Command Line Tools`。所以要写代码一定要安装哦！

那么如何安装呢？有两种方式。

苹果的开发集成工具是`Xcode.app`，其中就带着`Command Line Tools`，安装了`Xcode`相当于安装了`Command Line Tools`，那么我们可以直接在`App Store`下载`Xcode`。不过你打开一看，12G！！太大了吧。
`Command Line Tools`不过400MB多一点。如果你不从事苹果平台的软件开发，不需要使用`Xcode`，下载`Xcode`这么大的东西占电脑的存储空间，实在划不来。不过如果你已经安装了`Xcode`，那已经可以跳过这一步了。

- - - 

第二种方法是什么呢？

苹果也考虑了这种情况，所以在苹果官方开发者的网站上会有单独的命令行工具的下载。这个大小只有大概400MB，还算比较小（不过其实装好需要2.5G左右的空间，这个确实无法避免啦）

[在苹果开发者网站下载Command Line Tool](https://developer.apple.com/download/more/)

注意不要下载`beta`版，下载稳定版（于210110存在`12.5 beta`和`12.4`两个版本，下载`12.4`的版本）。

你也可以使用命令`xcode-select --install`来安装，效果和下载安装包后安装一样。但我个人感觉这种方式网络不太好，可能会出现问题，还是推荐大家在官网登陆`Apple账号`下载命令行工具。

### 安装Homebrew
工欲善其事，必先利其器。我们还需要安装`Homebrew`。`Homebrew`是什么呢？类比一下，我们安装有图形界面的软件，都是在`App Store`安装的。如果有应用发布了更新，`App Store`也会自动帮我们更新这些软件。`Homebrew`就好比命令行程序的应用商店，在`macOS`上，你需要什么命令行程序基本都可以通过`Homebrew`来安装；我们用`Homebrew`也可以查看哪些程序有了新的版本从而进行更新。用比较通俗的话来讲：`Homebrew`是`macOS`上最好用的包管理工具。

那么如何安装呢？可以到[Homebrew官网](https://brew.sh)找到安装的命令下载安装。然而官网用的服务器在国外，国内访问非常慢。我在知乎找到了一位仁兄写的脚本，能够帮我们一键安装`Homebrew`——[知乎｜Homebrew国内如何自动安装（国内地址）--金牛肖马](https://zhuanlan.zhihu.com/p/111014448)。复制他写的`安装脚本`，之后选择国内的源就大功告成了！

可以通过在终端输入命令`brew --version`来查看当前`brew`的版本以确定安装成功。

### 掌握终端和命令行的使用

如果你对终端和命令行完全是小白，那么我推荐你找一份教程熟悉终端和命令行的操作，之后再回到这份教程查看`python`的环境配置。比如查看我之前做的关于`macOS`终端和命令行的讲解。

[Bilibili | 认识mac的文件系统](https://www.bilibili.com/video/BV1ty4y1m7pZ)

[Bilibili | 认识程序](https://www.bilibili.com/video/BV1Sv4y1Z7Hd)

[Bilibili | 认识终端和shell](https://www.bilibili.com/video/BV1X5411n7tG)

## 安装python、用命令行执行python脚本

### 查看系统自带的python

首先呢，我们用`which python`和`where python`来查看`shell`如何解析我们的命令。打开文件夹，查看链接，发现链接到了系统自带的`2.7`版本的`python`上。

```py
import sys

print("Current python version:")
print(sys.version)
print()
print("Current python path:")
print(sys.executable)
print()

name = input("Please input your name: ")
print("Hello, " + name + "!")
```

用`python hello_world.py`来执行上述代码，发现多处都有问题，这是因为`python`的版本太老了

不要卸载这个版本，毕竟是系统自带的，卸载可能会导致系统出问题；我们重新安装一个新一些的版本就可以了（另外说不定你之后也会用到`python2`）

### 用Homebrew安装python3

```zsh
brew --help # 查看常用命令
```

```zsh
brew search [TEXT|/REGEX/] # 搜索程序（相当于在App Store搜索应用）
brew info [FORMULA...] # 查看某个程序的信息
brew install FORMULA... # 安装程序
brew update # 更新Homebrew自己
brew upgrade [FORMULA...] # 更新某（几）个程序
brew uninstall FORMULA... # 卸载删除某（几）个程序
brew list [FORMULA...] # 列出已经安装的程序（相当于打开了启动台）
```

我们会用到：

```zsh
brew search "py"
brew search "pyth"
brew install python3
brew info python3 # 查看某个程序的信息
brew list # 列出已经安装的程序（相当于打开了启动台）

brew upgrade python3 # 以后用来更新python3
```

```zsh
brew info python3
```

可以看到`python`的版本：`python@3.9: stable 3.9.1`

官网：`https://www.python.org/`

`brew`帮我们给`python3`添加了环境变量`Python has been installed as /usr/local/bin/python3`

可以看到`brew`安装的`python3`实际在这里：`/usr/local/Cellar/python@3.9/3.9.1_6`

它还推荐我们安装`python`第三方包的时候用命令`pip3 install <package>`，这些第三方包会被安装到这里：`/usr/local/lib/python3.9/site-packages`

### 用python3执行代码

由于`brew`已经自动帮我们把`python3`添加到了环境变量，所以我们用

```zsh
python3 hello_world.py
```

来执行代码。

这是打印的版本就是我们刚刚安装的`python3`，路径虽然与刚刚的安装路径对不上，但是进去一看，还是链接到了`brew`的安装路径。

### 创建python的链接

每次用`python`还得输`python3`，能不能只输`python`呢？能不能不要让`shell`把`python`这个单词解析到系统自带的`python2.7`呢？（注意：最好不要卸载`macOS`自带的`python2.7`，卸载的话可能会产生问题）

```zsh
open ~/.zshrc
```

```
alias python='python3'
alias pip='pip3'
```

这样你以后在`zsh`输`python`的时候，`shell`就会帮你找到`python3`这个命令，从而找到安装的`python3`解释器（注：这只对`zsh`有用，因为` ~/.zshrc`是`zsh`的用户配置文件）

再次尝试`which python`和`where python`和`python hello_world.py`

### 用绝对路径和相对路径执行python脚本

用`chmod a+x hello_world.py`给脚本执行权限，复制`hello_world.py`的绝对路径，回车。使用相对路径再次进行尝试。发现都失败。

这里`shell`将你写的`python`脚本当作`shell`脚本来执行了，所以里面的东西它完全不认识。（注意：后缀名`.py`仅仅是文件名的一部分，`shell`只会将其当作文件名的一部分，不会因为有了这个后缀`shell`就把这个文本文件当作`python`脚本）

那么如何让`shell`认识这是一个`python`脚本？既然`brew`已经将我们新安装的`python3`放到了环境变量里，所以我们直接用环境变量告诉`shell`需要调用的`python`解释器就好了。在脚本的第一行加上：

```zsh
#!/usr/bin/env python3
```

（原因：`python`解释器在不同系统中可能被安装于不同的目录，如在 `macOS` 中装在 `/usr/local/bin/python`，但是在 `linux` 上装在 `/usr/bin/python` 中；`env` 可以在系统的 `PATH 目录 ` 中查找所需要的解释器，因此你在 `Mac` 上写的 `py` 脚本直接复制到 `Linux` 一样可以执行（`Windows` 不是这么执行脚本的所以我也不清楚复制过去行不行哈））

再次尝试绝对路径和相对路径，成功。

## 配置VS Code写python代码的环境

### 下载VS Code

在[微软VSCode官网](https://code.visualstudio.com)直接下载`macOS`平台的最新版本即可。下载到安装包解压后将蓝色的`VS Code`拖到应用程序的文件夹

### 安装python插件

### 在settings.json中添加

```json
  ////// 调试Python代码（F5） //////
  // Path to Python, you can use a custom version of Python 
  // by modifying this setting to include the full path.
  "python.pythonPath": "python3", // 直接用命令就好（因为zsh已经知道python3指的就是那个解释器）。你也可以更改为python3解释器的安装路径（但是我推荐你直接写python3）
```

### 用VS Code调试python代码

首先要明白`python`是解释型语言，这和`C/C++`等编译型语言不一样，它是一行一行执行的。这个一行一行执行的过程，就相当于你在`debug`。

点击`F5`（或触控栏上的播放键，或在左侧边栏找到播放键，或者在菜单栏找到开始调试），`python`代码就会开始运行。

为了少一步点击，我们在`.vscode`文件夹中创建`launch.json`，点击添加配置自动生成。

```json
{
  "configurations": [
    {
      "name": "Python Debug",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    }
  ]
}
```

`name`可以改，会在左侧显示。`type`、`request`不动。`program`就是你写的脚本的路径（按⌘I查看其他的可用的配置文件变量）。`console`也可以通过⌘I选取喜欢的终端（`integrated terminal`指`VS Code`下方的集成终端（推荐），`external terminal`指系统自带的终端，另一个貌似是只读的，不推荐）。按⌘I查看其他的选项。

尝试使用断点阻碍代码运行。如果是外置终端，左右分屏。如果是集成终端，注意输出不会自动翻页。

### 安装其他插件

VS Code图标：`vscode-icons-mac`

彩虹括号：`Bracket Pair Colorizer`

彩虹缩进：`indent-rainbow`

### 安装插件Code Runner

我们刚刚使用`VS Code`的调试器（`VS Code`调试的时候就带上了调试器）进行代码的执行，可以发现一卡一卡的，很难受。有的时候我只希望运行出个结果，不需要中间停下来。

在插件商店安装`Code Runner`

在`settings.json`中添加下面的语句：

```json
  ////// Code Runner执行Python代码（⌘R） //////
  "code-runner.executorMap": {
    "python": "python3",
  },
  // Whether to save the current file before running.
  "code-runner.saveFileBeforeRun": true, // run code前保存
  // Whether to save the current file before running.
  "code-runner.runInTerminal": true, // 设置成false会在"OUTPUT"中只读输出，无法输入数据
  // Whether to preserve focus on code editor after code run is triggered.
  "code-runner.preserveFocus": false, // 若为false，run code后光标会聚焦到终端上。如果需要频繁输入数据可设为false
  // Whether to clear previous output before each run.
  "code-runner.clearPreviousOutput": true, // 每次run code前清空属于code runner的终端消息，默认false
  // Whether to ignore selection to always run entire file.
  "code-runner.ignoreSelection": false, // 只跑选中的n行代码
```

挨个尝试每个选项（先更换快捷键）

## 结语

希望这份教程能对大家有帮助！

如果还想深入了解如何在`VS Code`中更好的写`python`，可以查看[VS Code官方文档](https://code.visualstudio.com/docs)

## 其他

[CSDN | VS Code python 包导入报错 unresolved import 的解决措施](https://blog.csdn.net/qq_45379253/article/details/113879292)
