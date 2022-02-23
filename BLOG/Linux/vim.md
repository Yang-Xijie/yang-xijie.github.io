# Vim 学习笔记

> Author: 杨希杰 [Yang Xijie](https://github.com/Yang-Xijie)
> 
> Written on: 210419
> 
> Notes: 记录了vim一些简单实用的操作

## 基本

〇 编辑 退出

`i` `Esc`（进入/退出编辑模式）

`ZZ(:wq)` `ZQ(:q!)`（保存退出/舍弃更改退出）

〇 文件

`:w`（保存）

`:w <filename>`（另存）

`:<start_line>,<end_line> w <filename>`（指定行另存）

`:!ls`（不退出vim用bash在当前文件夹下执行ls命令）

〇 行号

`:set nu`（显示行号）

`:set nonu`

## 移动

### 移动页面

〇 翻页

⌃F ⌃B

〇 翻半页

⌃D ⌃U

〇 滑动

⌃E ⌃Y

〇 移动cursor所在行到屏幕上/中/下

`zt` `zz` `zb`

### 移动cursor

〇 下/上

`j` `enter` `k`

`<n>enter` `<n>j`（下移n行）

`+` `-`

〇 左右

`h` `l` `space`

`<n>space` `<n>l`（右移n个字符）

`w` `b`（词）

〇 行尾/行首

`$` `0`

〇 文档首行/末尾

`1G` `G`

`<n>G`（文档第n行）

〇 屏幕上/中/下

`H` `M` `L`

〇 括号两侧

`%`

## 删除 复制 粘贴

### 删除 / 剪切

〇 `d<移动cursor操作>`

如：`d3h`（向左删3下） `dw`（向后删除一个词） `d$(D)`（删除到行末） `dG`（删除到文档尾） `1GdG`（删除全部） `dL`（删除屏幕下半内容）

〇 ⌫ / fn ⌫ 

`X(dh)` `x(dl)`

〇 行

`dd`（删除当前行）

`<n>dd`（向下删除n行）

〇 选中删除

`v 移动cursor d`（先高亮选中再删除）

注：⌃V（块选中）

### 复制

将上面删除中的`d`换为`y`即可

### 粘贴

向后/前粘贴

`p` `P`

### 撤销 重做 重复

`u` ⌃R `.`

## 编辑

〇 缩进

`>>` `<<`

## 搜索 替换

〇 用正则表达式搜索

向后 向前

`/<regular expression> enter`

`?<regular expression> enter`

继续搜索

`n N`

〇 用当前光标所在位置词语搜索

向后 向前

`* #`

〇 替换

将当前行的所有expr1替换为expr2

`:s/<expr1>/<expr2>/g`

将两行之间的所有expr1替换为expr2

`:<start_line>,<end_line>s/<expr1>/<expr2>/g`

将全文档的所有expr1替换为expr2

`:%s/<expr1>/<expr2>/g`

## References

[菜鸟教程｜vim](https://www.runoob.com/linux/linux-vim.html)

[Graphical vi-vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
可下载到`vim键位表`(svg)及其`中文版`(gif)、`分lesson的键位表`(svg)、`合集`(PDF)

[CSDN | vim 文件查找与替换](https://blog.csdn.net/cbaln0/article/details/87979056)
