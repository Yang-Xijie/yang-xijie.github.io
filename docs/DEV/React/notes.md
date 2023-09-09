# React Notes

## 前端与桌面端的区别

- 前端自带 ScrollView，只要你往上加 Component，默认都是往下一直叠加的。
- 前端需要考虑 Responsive，而移动端可以只考虑 Adaptive（一个一个机型适配也不是不可以）。前端需要判断用户界面的大小来呈现不同的内容，但像移动端就总是那么大的屏幕，桌面端可以限制最小的窗口大小。前端在不同界面大小适配上花的工夫还是挺多的。

## React

https://react.dev

- [Quick Start](https://react.dev/learn)
- [Start a New React Project](https://react.dev/learn/start-a-new-react-project)
    - 官方并不推荐使用 Vite 开始新项目。但是对于初学以及 SPA 来说，Vite+React 应该是最好的新建项目的方式。

## SPA 与 Next 的区别

[Blog | Create React App 与 Next.js 的区别](https://prismic.io/blog/create-react-app-cra-vs-nextjs) 简单来说，做小的展示项目用就选；遇到性能瓶颈、做前端大项目首选 Next.js。

但是，我应该不会做前端的大项目了，科研的话主要就是写能在浏览器看的展示类 app，也就是 SPA。

## Vite

https://vitejs.dev

创建项目用 [Vite](https://vitejs.dev) 而不是 [CRA](https://create-react-app.dev)，因为 CRA 实在是太老了，默认模板里面一堆不需要的东西；Vite 简洁明晰而且高效，体验起飞。

## TS

https://www.typescriptlang.org

TS 是必须的。在写 WebGPU 相关的代码时我发现，自己写代码，没类型完全 OK，JaveScript 毕竟是脚本语言。但是当使用别人的库的时候，没有类型那是真的痛苦。而且，用 TS 很简单，JS copy paste 改一改就行了。
