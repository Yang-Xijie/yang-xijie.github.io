# macOS 使用 tree 命令和访达进行任务管理

> 笔者手上事儿比较多，经常要记录接下来要做的事情防止忘记。在macOS上，我并没有发现很好的任务/to-dos管理软件。之前一直在用macOS自带的便笺，放到桌面上；但是这样很不优雅和美观，遮挡桌面不说，给任务分组、更改任务分组也很麻烦（剪贴粘贴）。
> 
> 于是就在想自己开发一个macOS app实现一下吧，可是我Swift还没学呢hhh
> 
> 某天晚上突然想到这不就是文件目录吗？文件夹是分组，里面的文件是任务。突然就想起来访达和tree命令，这不就是天然的任务管理吗？但是简单尝试后发现，tree命令对中文、空格的支持很不好，显示的格式有点差。于是想着去找找别的tree命令。GitHub上一搜发现个人实现的tree命令很多。在[kddeisz/tree](https://github.com/kddeisz/tree.git)这个项目中，作者用多种语言实现了tree命令。我尝试了shell版和C版，觉得还是python版好用。
> 
> 以下是我的使用方法：

## 使用配置

```bash
cd [dir_git]
git clone https://github.com/kddeisz/tree.git
cd tree
mv tree.py [dir_TASK]/.tree.py
echo "alias task='cd [dir_TASK] && [dir_TASK]/.tree.py'" >> [file_runcom]
```

其中：

- `[dir_git]` -> clone GitHub项目时的目录：`/Users/yangxijie/yxj/CODE/Git`
- `[dir_TASK]` -> 存放任务的根目录：`/Users/yangxijie/Desktop/TASK`
- `[file_runcom]` -> shell启动时读取的配置文件：`~/.zshrc`

## 使用方法 命令行

切换到根目录并显示所有任务：`task`

- 新建分组：`mkdir [group]`
- 新建任务：`touch [group]/[task]`

（其中`[task]`为任务内容，推荐不带后缀名；推荐使用英语，因为shell按⇥可以自动补全，用中文就意味着需要切换输入法不够效率）

添加备注：可以`echo [comment] >> [group]/[task]`、查看使用`cat [group]/[task]`（但是这样你不知道哪个任务有注释，可以考虑在`[task]`中添加信息来说明此任务有备注。但是我更推荐将备注直接写到文件名`[task]`里）

显示分组内的任务：`task [group]`

- 更改任务：`mv [group]/[task] [group][task_new]`
- 移动任务：`mv [group]/[task] [group_new]`
- 删除任务：`rm [group]/[task]`
- 删除分组：目录中无任务：`rmdir [group]`；删除目录及目录下的任务：`rm -rf [group]`

## 使用方法 访达

切换到根目录查看任务：双击打开

- 新建分组：新建文件夹
- 新建任务：复制已经有的任务进行重命名（因为访达不能直接新建文件）

- 添加备注：推荐将备注直接写到文件名`[task]`里

- 更改任务：重命名
- 移动任务：拖移文件
- 删除任务：`⌘⌫`
- 删除分组：`⌘⌫`

## 效率神器Manico推荐

需要命令行操作就要打开终端，那么如何快速打开终端呢？ Manico

在[App Store](https://apps.apple.com/cn/app/manico/id724472954?mt=12)下载

免费版本有使用限制，30元购买无限制使用（划得来）

只需要给终端设置一个全局快捷键就可以快速打开啦

## 使用的python脚本

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import os
import sys

class Tree:
    def __init__(self):
        self.dirCount = 0
        self.fileCount = 0

    def register(self, absolute):
        if os.path.isdir(absolute):
            self.dirCount += 1
        else:
            self.fileCount += 1

    def summary(self):
        return str(self.dirCount) + " directories, " + str(self.fileCount) + " files"

    def walk(self, directory, prefix = ""):
        filepaths = sorted([filepath for filepath in os.listdir(directory)])

        for index in range(len(filepaths)):
            if filepaths[index][0] == ".":
                continue

            absolute = os.path.join(directory, filepaths[index])
            self.register(absolute)

            if index == len(filepaths) - 1:
                print(prefix + "└── " + filepaths[index])
                if os.path.isdir(absolute):
                    self.walk(absolute, prefix + "    ")
            else:
                print(prefix + "├── " + filepaths[index])
                if os.path.isdir(absolute):
                    self.walk(absolute, prefix + "│   ")

directory = "."
if len(sys.argv) > 1:
    directory = sys.argv[1]
print(directory)

tree = Tree()
tree.walk(directory)
print("\n" + tree.summary())
```
