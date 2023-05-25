# 软件崩溃分析

220331 我提交了一版macOS app之后，app review得到了如下消息：

> Guideline 2.1 - Performance - App Completeness
> 
> We were unable to review your app as it crashed on launch on Mac running macOS 12.3. We have attached detailed crash logs to help troubleshoot this issue.

哦 这可真是让人沮丧，明明在我电脑上没任何问题，指令集架构和系统版本都一样。

但是我又没办法不信，reivew team 确实给出了 crash log：

> Rejection Attachments:
>
> ExSticky-2022-03-30-154359.ips Preview Download

那就只好分析crash log了。

首先明确，app跑起来之后是一堆的指令（比如 `0x1003b54a2 0x1003a6000`）。我们要想从这些人看不懂的指令里面来找到我们程序的高级语言中对应的位置，我们需要先做符号化。下面是原始的崩溃日志：

```
$ ips_path="/Users/yangxijie/Downloads/ExSticky-2022-03-30-154359.ips"
文件重要内容
Thread 0 Crashed::  Dispatch queue: com.apple.main-thread
0   ExSticky                      	       0x1003b54a2 0x1003a6000 + 62626
1   ExSticky                      	       0x1003b54c8 0x1003a6000 + 62664
Binary Images:
       0x1003a6000 -        0x1003c9fff com.yangxijie.exsticky.beta (2.2) <55274427-46af-3910-94ce-176949ff64ce> /Applications/ExSticky.app/Contents/MacOS/ExSticky
```

首先找到你提交的那个版本的确切archive文件，使用Xcode上传的话，在Xcode的Organizer中就有。可以再去人一下两个uuid是否一致：

```
$ dsym_path="/Users/yangxijie/Library/Developer/Xcode/Archives/2022-03-30/ExSticky 2022-3-30, 21.23.xcarchive/dSYMs/ExSticky.app.dSYM/Contents/Resources/DWARF/ExSticky"
$ dwarfdump --uuid $dsym_path
UUID: 55274427-46AF-3910-94CE-176949FF64CE (x86_64) /Users/yangxijie/Library/Developer/Xcode/Archives/2022-03-30/ExSticky 2022-3-30, 21.23.xcarchive/dSYMs/ExSticky.app.dSYM/Contents/Resources/DWARF/ExSticky
```

然后用atos工具来做符号化：

```
$ atos -arch x86_64 -o $dsym_path -l 0x1003a6000 0x1003b54a2 + 62626
TextWindow.close() (in ExSticky) (TextWindow.swift:41)
+
62626
$ atos -arch x86_64 -o $dsym_path -l 0x1003a6000 0x1003b54c8 + 62664
@objc TextWindow.close() (in ExSticky) (<compiler-generated>:0)
+
62664
```

可以看到大致是 `TextWindow.close()` 函数的问题。对应看代码去优化就可以了。

至于为什么苹果那边测试过不了，自己电脑上却没问题，这个多半是因为优化器，还有个人电脑上的权限会更高一些，有些问题可能不会显示而是直接被操作系统处理掉了。
