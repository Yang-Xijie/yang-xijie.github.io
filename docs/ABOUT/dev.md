# 文章编写指南

## 语言支持

并不支持英文 因为文章主要使用中文 访问者主要是中国人

## index

最开始打开网站 也就是通过链接 <https://yang-xijie.github.io/> 访问时 会先打开 `/docs/index.md` 这时访问者点击左上角按钮展开目录会先看到大的分类

因为不希望用户之后找不到这个页面 所以 `/docs/ABOUT/index.md` 下面的内容与 `/docs/index.md` 的内容一致

每个nav的tab下有一个`index.md` 点击tab会线跳转到这些`index.md`

## metadata

```
---
title: <title>
description: <description>
tags:
  - <tag1>
  - <tag2>
---
```

有三个标题：

- nav中指定的标题：导航时显示的标题 可以因为层次结构而省略
- 文章在上方通过`---`段设置的标题：下滑后出现的标题为此标题
- 文章第一个#标题：也只能有一个 或者整篇文章都没有 [参考](https://github.com/squidfunk/mkdocs-material/issues/818) 否则右侧目录无法正常显示 
    - 如果设置了`---`段的标题 可以不使用 
    - 如果未设置`---`段的标题 下滑后出现的标题为nav的标题
    - 整体考虑不太需要h1 使用`---`段设置title即可
