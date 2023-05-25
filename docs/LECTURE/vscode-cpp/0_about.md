# 在macOS上用VSCode写C++代码 0 简介

## 简介

系列教程——如何在`macOS`上使用`VS Code`优雅的写`C++`代码。教你从零开始配置你自己的`C++`编程环境。

注意：我推荐大家先查看[极速版教程](https://www.bilibili.com/video/BV14y4y1m7Bs)。你如果对其中所说的东西都很了解那么是没有必要看我这个系列教程的。这份系列教程主要针对大一刚刚开始学习程序设计而且使用`mac`电脑的同学，因此我大概花了一半时间来讲终端`shell`和命令（因为大学往往会忽略讲解这些东西）。如果教程中有你已经了解的地方，你可以直接跳过某节或某几节课；由于这是我第一次出类似的教程，也会有一些不足的地方，也希望大家在评论区提出来；如果你觉得我的语速慢，请开启倍速。谢谢！希望这份教程能让大家有所收获。

点击页面左上角的图标可以切换页面查看[此课程的讲稿](./1_前言和课程说明.md)。

点击下方的链接跳转[Bilibili视频教程](https://space.bilibili.com/24502827)。

## 在Bilibili查看视频教程

注：所有视频录制及上传分辨率均为`3360x2100`，如果观看时感到视频模糊，请调整画质到`4K 超清`；由于视频比例为`16:10`，建议使用相同比例的显示器全屏播放以获得最佳观看体验。

[1 前言和课程说明](https://www.bilibili.com/video/BV1UK4y1W7oM)

[2 认识mac的文件系统](https://www.bilibili.com/video/BV1ty4y1m7pZ)

[3 认识程序](https://www.bilibili.com/video/BV1Sv4y1Z7Hd)

[4 认识终端和shell](https://www.bilibili.com/video/BV1X5411n7tG)

[5 开启VS Code的大门（上）](https://www.bilibili.com/video/BV1g54y1s74Z)

[5 开启VS Code的大门（下）](https://www.bilibili.com/video/BV17U4y147eo)

[6 VS Code代码运行自动化](https://www.bilibili.com/video/BV14K411u7SN)

[7 用VS Code调试Cpp代码](https://www.bilibili.com/video/BV13y4y1m7WK)

[8 课程回顾](https://www.bilibili.com/video/BV1Up4y1x7ve)

[极速版](https://www.bilibili.com/video/BV14y4y1m7Bs)

## 附

很用心做的一期教程，因为觉得很有这么做的必要！做这份教程的原因我在第一课和第八课都有提到～

说实话，录教程真的 太 累 了。`1倍`时间的视频，构思大概会花掉`2倍`，写讲稿和上传讲稿、修改讲稿大概花`5倍`时间，录制一般花`1倍`时间（但是紧张的时候差不多就得`1.5倍`），倒入FCPX检查一遍大概`1.5倍`时间，导出和上传视频、写简介、写评论加起来平均花掉`3倍`时间；整个算下来差不多是`12.5倍`的时间。希望这么做是值得的，希望能帮到大家！

如果大家觉得有帮助，还请把这份教程推荐给身边的同学哦！

### 想对使用Windows的同学说的话

之前提到“应该”会出一个`Windows`版，但是做完这份教程觉得，做教程太花时间了，我大概是没有经历再出一份相同思路的`Windows`版教程；另外，我对`Windows`系统可能也没有那么熟悉，做出来的教程质量很难保证。如果可以，我非常希望有熟悉`Windows`的同学出一份相应的视频教程，帮助大一新入学的同学们配置好属于自己的`C++`编程环境。

另外，即使你在使用`Windows`系统，也可以通过我的这份教程从思路上了解配置的过程，让你的环境配置更顺利（也许）！

### 其他想说的话

这份教程是`AS-IS`的，意思是说，这份教程我做出来就放在这里它就是这个样子。至于你看不看这份教程，这是你自己的选择。如果你看了这份教程然后觉得我讲的不行，那我觉得可能你并不适合这份教程，或者确实我这份教程做的不好；但请注意这是你自己的选择。如果你想给我的课程提一些建议，我非常欢迎，不过如果可以，我希望你的语气能委婉一些。

提问前请先仔细阅读[提问的智慧（中文版）](https://github.com/tvvocold/How-To-Ask-Questions-The-Smart-Way)（the original version in English [How To Ask Questions The Smart Way](http://www.catb.org/~esr/faqs/smart-questions.html) ）。