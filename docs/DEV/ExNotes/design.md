# ExNotes 设计文档

> Author: [Yang-Xijie](https://github.com/Yang-Xijie)
> 
> All rights reserved.
>
> 220125

## 目标

希望能做出与Nb书写体验相近的Apple Pencil笔记软件。

核心：

* Apple Pencil汉字书写
* 使用Metal实现低延时渲染
* 滚动连续翻页
* PDF导出
* PDF导入与标注

## 开始页

### Tags

可折叠

* Pinned: 最近都在做的比较重要的笔记
* Bookmarks：很重要 但不是最近在做的
* Favorites：很喜欢的东西 但是不会经常去看

### 抽屉

不可折叠

### 资料库

可折叠

默认资料库：My/我的 可以改名字/图标 不可删除

软件第一次开启给数据库中放入默认资料库，两个文件夹
* ExNotes 里面放说明书
* Drafts 里面随便放几个文件

#### 手势操作

不支持左滑

资料库长按菜单（短按拖拽）：

* 新建资料库
* 新建文件夹
* 重命名（Alert）——不能自己设置图标 颜色用tintColor
* 删除（Alert）红色 需要确认
    * 删除该资料库内所有文件夹中的文件、然后删除该资料库
    * 移动该资料库内所有文件夹至默认资料库、然后删除该资料库
    * 取消

### 文件夹

#### 手势操作

不支持左滑

文件夹长按菜单（短按拖拽）：

* 新建文件夹（在当前文件夹所在的资料库内新建文件夹）
* 设置（page sheet）
    * 重命名
    * 设置图标（SF Symbol名称 / 颜色）
* 移动（page sheet） 到其他文件库
* 删除文件夹（Alert）红色 需要确认
    * 删除其中的所有文件
    * 取消

## 笔记

### 上方工具按钮

* 关闭
* 撤销，重做（有了之后再出现）
* 笔，橡皮，套索
* 添加
    * 形状
    * 文字（暂不支持）
    * 图片
    * 照相
    * Document Scan
* 信息
    * pin bookmark favorite delete 四个大图标
    * 页视图
    * 大纲视图
    * Lines
    * Backgrounds
* Share
    * PDF
    * PNG
    * Print

### 排序

Notes (sort by createdTime/name/modifiedTime des/as)

### 手势操作

左滑 pin bookmark favorite delete

笔记长按菜单（短按拖拽）：

* TODO

- - -

## 设置

* tint color
* 暗夜模式
* 撤销手势：三指左滑或者两指轻点
* 备份所有文件到iCloud或本地磁盘
