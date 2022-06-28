# GitHub Pages

简单来说，`GitHub Pages` 是可以轻松快速部署静态网站的方式，你可以在 GitHub 的每一个仓库创建一个对应的静态网站，存放说明或文档。

通俗来说，就是白嫖GitHub的服务器来建站，GitHub Pages，与Git管理超搭，免费不说，还相当稳定的，而且有全球的CDN加速，也没被墙，我只能说真爽。有了自己的网站<https://yang-xijie.github.io>之后，我几乎就很少在各种平台发博客了。

- https://pages.github.com
- [About GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)
    - [Types of GitHub Pages sites](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites)

这里一定要注意：个人用户只有两种 GitHub Pages 网站的类型：一种是 `user`(用户)，一种是`project`(项目)。

`user`类型的网址只能对应唯一的用户，而且仓库的名字必须为 `<username>.github.io`，对应的网址为 `http(s)://<username>.github.io`。

`project`类型的仓库则可以新建很多，只要仓库的名字不为 `<username>.github.io` 即可，对应的网址为 `http(s)://<username>.github.io/<repository>`。

根据这两种类型，建站可以有两种策略：

- 只创建一个user仓库`<username>.github.io`，所有的文章都放在这个仓库中。
    - 优点：只有一个仓库维护方便
    - 缺点：你的个人账户再新建`project`类型的仓库大概率会与这个user仓库冲突。但我感觉一般对于个人来说 一个仓库也完全够用。
- 不创建user仓库，需要静态网站时新建多个`project`类型的仓库
    - 优点：仓库不限量 仓库之间互不冲突 可以使用不同的框架
    - 缺点：多个仓库维护困难

选择哪种仁者见仁智者见智吧
