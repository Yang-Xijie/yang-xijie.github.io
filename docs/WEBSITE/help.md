# 文章编写帮助

## 语言支持

并不支持英文，因为文章主要使用中文，访问者主要是中国人。

## index

最开始打开网站，也就是通过链接 <https://yang-xijie.github.io/> 访问时，会先打开 `/docs/index.md`，这时访问者点击左上角按钮展开目录会先看到大的分类。

因为不希望用户之后找不到这个页面，所以 `/docs/WEBSITE/index.md` 下面的内容与 `/docs/index.md` 的内容一致。

每个 nav 的 tab 下有一个 `index.md`，点击 tab 会先跳转到这些 `index.md`。

所以 如下提示可以忽略：

```
INFO - The following pages exist in the docs directory, but are not included in the "nav" configuration:
     - index.md
```

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

## title

有三个标题:

- `nav-title`: 在 `mkdocs.yml` 的 `nav` 中指定的标题
    - 导航时显示的标题，可以因为层次结构而省略。
- `meta-title`: 文章在最上方通过 `---` 段设置的标题
    - 下滑后出现的标题为此标题。
- `h1-title`: 文章第一个 `#` 标题
    - 只能有一个，或者整篇文章都没有 [参考](https://github.com/squidfunk/mkdocs-material/issues/818)，否则右侧目录无法正常显示。
    - 如果设置了 `---` 段的标题，可以不使用。
    - 如果未设置 `---` 段的标题，下滑后出现的标题为 nav 的标题。
    - 如果没有这个标题，会自动将 nav 的标题拿过来。

推荐的使用方法是，设置简洁的 `nav-title` 用来导航，`meta-title` 和 `h1-title` 使用相同的标题表述文章内容。或者只设置 `h1-title`。

## 图片

```
![](./media/xxx.png){width="300"}

![](./media/xxx.png){width="50%"}
```

注意:

- 有些外链图片没有 token 是无法直接获取的。
- 如果希望图片并排，删掉两个图片中间的空行。
