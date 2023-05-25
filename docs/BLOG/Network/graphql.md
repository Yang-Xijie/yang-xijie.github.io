# iOS 网络服务应用尝试

> Written by 杨希杰 on 210324

## GraphQL

### Introduction

一种前后端数据请求/交互的风格/标准/规范。是有着大公司做靠山、较新的查询语言规范，是一种基于图的查询语言。对比原有的REST请求风格，GraphQL能够让你每次都获取到不多不少的数据，结合社区的工具，几乎可以省掉后端的开发团队，让你的项目开发效率大大提升。

> GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

`GraphQL clients`是嵌入在前端/需要在前端导入的一个工具，这个工具能帮助你在UI中引入数据查询，让你用GraphQL的语句来向后端的`GraphQL server`发送请求。

> **GraphQL clients** can help you handle queries, mutations, and subscriptions to a **GraphQL server**. They use the underlying structure of a GraphQL API to automate certain processes. This includes batching, UI updates, build-time schema validation, and more.

### Resources

* [GraphQL](https://graphql.org)
    * GraphQL官网
* [GraphQL｜中文官网](https://graphql.cn)
    * 推荐看英文官网
* [GraphQL | Learn](https://graphql.org/learn/)
    * **IMPORTANT**
    * 入门GraphQL

## GraphQL Client｜Apollo Client (iOS)

```
Apollo is the industry-standard GraphQL implementation, providing the data graph layer that connects modern apps to the cloud.
```

* [Apollo](https://www.apollographql.com)
    * Apollo官网
* [Apollo docs｜Apollo Basics](https://www.apollographql.com/docs/)
    * **IMPORTANT**
* [Apollo Client | iOS](https://www.apollographql.com/docs/ios/)
    * **IMPORTANT**
    * [GitHub | Apollo Client | iOS](https://github.com/apollographql/apollo-ios)

## GraphQL Server｜Hasura + Databse

`GraphQL Server`处理前端从`GraphQL Client`发送的`GraphQL请求`，在数据库中获取相应的数据并返回到前端/客户端。

这里`Hasura`相当于一个控制台，帮你在中间操作数据库；同时`Hasura`也提供可视化的控制台，让数据库的管理变得方便。

> The Hasura GraphQL engine makes your data instantly accessible over a real-time GraphQL API, so you can build and ship modern apps and APIs faster. Hasura connects to your databases, REST servers, GraphQL servers, and third party APIs to provide a unified realtime GraphQL API across all your data sources.

* [Hasura](https://hasura.io)
    * Hasura官网
* [Hasura | Tutorials](https://hasura.io/learn/)
    * **IMPORTANT**
    * 教程资源整合，包括了从GraphQL到Hasura的所有内容
    * 具体见下方
* [Hasura | GraphQL Engine Documentation](https://hasura.io/docs/latest/graphql/core/index.html)
    * **IMPORTANT**
    * 关于Hasura的部署使用的文档
* [GitHub | GraphQL engine](https://github.com/hasura/graphql-engine/)
    * [实时聊天软件展示](https://realtime-chat.demo.hasura.app/)
* [实时聊天软件repo](https://github.com/hasura/graphql-engine/tree/master/community/sample-apps/realtime-chat)
    * [其他的一些sample-app](https://github.com/hasura/graphql-engine/tree/master/community/sample-apps)
* [Hasura Cloud](https://cloud.hasura.io)
    * Hasura Cloud相当于一个搭建好的Hasura平台，可以直接通过在其中创建的project开启console。
    * 注意这个是不带数据库的，你需要将一个已有的postgres数据库链接到Hasura上（这里数据库可以用Heroku免费的，但我并不清楚有这个的使用是不是有限制）
    * 免费版的可以自己尝试玩，但是有流量限制（1G/month），一分钟也只能请求60次
    * 标准版流量可叠加（20G/month，2刀 per additional GB），但没有请求限制。每月100刀
    * [Hasura Cloud Documentation](https://hasura.io/docs/latest/graphql/cloud/index.html)

其他：

* Hasura-cli
    * 记录每次在Hasura控制台对数据库的操作，方便对项目进行迁移
* 跑在服务器Docker上的postgres
    * 也可以在服务器上安装postgres
    * 需要将数据库的地址或服务端口交给Hasura

## 对象存储服务

图片和视频等资源存储在哪里？数据库里？服务器的文件路径下？云服务厂商提供的对象存储服务上？

## 登录验证

token、jwt需要去了解一下，密码加盐如何前后端中分别实现？

## Hasura Tutorial

[Hasura | Tutorial](https://hasura.io/learn/)

* 一条龙的教程资源整合。非常详细的文档。总之就是非常推荐
* [GitHub｜Hasura | Tutorials](https://github.com/hasura/learn-graphql)
    * 所有教程代码的存放仓库

### Introduction to GraphQL

[Hasura Tutorial｜GraphQL intro](https://hasura.io/learn/graphql/intro-graphql/introduction/)

* **IMPORTANT**
* `GraphQL`简介，包括：`GraphQL`是什么，`GraphQL`与`REST`的区别，`GraphQL`中的核心概念和术语，`GraphQL`三种请求数据的方式，`GraphQL Clients`和`GraphQL Servers`

### Frontend GraphQL Tutorial

[Hasura Tutorial｜GraphQL Client with iOS](https://hasura.io/learn/graphql/ios/introduction/)

* **IMPORTANT**

### Hasura Tutorials

[Hasura Tutorial｜Hasura Basics](https://hasura.io/learn/graphql/hasura/introduction/)

* **IMPORTANT**

[Hasura Tutorial｜Auth Patterns with Hasura](https://hasura.io/learn/graphql/hasura-auth-slack/introduction/)

* **IMPORTANT**

[Hasura Tutorial｜Hasura Advanced]()

* **IMPORTANT**

### Sample Apps

[Hasura Tutorial｜WhatsApp Clone](https://whatsapp-clone.demo.hasura.app/sign-in)

* [GitHub｜whatsapp-clone-typescript-react](https://github.com/hasura/graphql-engine/tree/master/community/sample-apps/whatsapp-clone-typescript-react)

[Hasura Tutorial｜React to-do app](https://react-apollo-todo.demo.hasura.app)

* [GitHub｜todo-auth0-jwt](https://github.com/hasura/graphql-engine/tree/master/community/sample-apps/todo-auth0-jwt)
* [GitHub｜react-apollo-todo](https://github.com/hasura/graphql-engine/tree/master/community/sample-apps/react-apollo-todo)
