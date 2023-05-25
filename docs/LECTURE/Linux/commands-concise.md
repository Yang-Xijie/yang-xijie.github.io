# 命令行入门精简版

> 此份教程主要面向非开发人员，以介绍为主。

## 打开命令行

### Windows

桌面右键 `Git Bash Here` 打开 `Git Bash`。

### macOS

聚焦搜索 `cmd 空格` 搜索 `终端` 或 `terminal` 打开终端。

## 常用命令

### 普通命令

- `date` 了解命令行可以调用一个程序
    - 查看`date`的帮助文档：`date --help` (Git Bash) 或 `man date` (macOS / Linux)
    - 格式化打印时间：`date "+%m/%d"` 了解程序可以接受输入 对应有输出
- `echo` 原封不动打印出输入的内容
- `clear` 清屏
- `history` 查看之前敲过的命令

### 文件系统相关

- 目录
    - 了解文件系统是一个树状的结构
    - `pwd` print working directory
        - 显示shell的工作目录
    - `ls` list
        - 列出shell的工作目录下的所有文件夹和文件
    - 文件路径的表示
        - 根目录 `/`
        - 当前目录 `.` 上级目录 `..` 上上级目录 `../..`
        - 家目录 `~`
    - `cd` change directory
        - 切换shell的工作目录
- 文件夹
    - `mkdir` make directory
        - 创建一个文件夹 如 `mkdir new_folder` 注：不要在文件夹内带空格
- 文件
    - `touch`
        - 创建一个纯文本文件 如 `touch a.txt`
    - `cat` concatenate
        - 显示一个文本文件的内容 如 `cat a.txt`
    - `mv` move
        - 移动一个文件到另一个路径 如 `mv a.txt ../a.txt` 将文件移动到上层文件夹
        - 重命名文件 如 `mv a.txt b.txt`
    - `cp` copy
        - 复制文件到另一个文件 如 `cp a.txt b.txt`
    - `rm` remove
        - （注意 `rm` 会直接删除 使用时一定当心）
        - 删除文件 如 `rm a.txt`
        - 批量删除文件 如 `rm *.txt` 删除所有的 `txt` 文件
        - 删除文件夹内所有内容 如 `rm -r folder`

安装 `VS Code` 之后可以用 `code` 命令打开一个文件夹或文件，如 `code new_folder` `code README.md`

## Shell使用技巧

### 常用技巧

- Tab补全
    - 命令输入到一半时补全命令
    - `cd`时补全路径 `cat`时补全文件名 等
- `ctrl C`
    - 清除输入的命令
    - 结束正在运行的程序
- 按上键调出之前的命令
- 在进入一些“窗口”时（如 `git log` 之后的“窗口”），可以在英文输入法下按 `q` 退出

### 调整文字大小

- `Windows - Git Bash` 右键菜单栏，点击 `Options` 里面可以调整字体大小。更方便的是使用 `ctrl -` 和 `ctrl =` 来进行控制字体大小。
- `macOS - Terminal` 用 `cmd ,` 打开设置，在 `Profiles > Default > Text > Font` 处调整字体大小。更方便的是使用 `cmd -` 和 `cmd =` 来进行控制字体大小。
