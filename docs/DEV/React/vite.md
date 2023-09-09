# Vite+React+TS 创建新项目

## 创建方式

```sh
npm create vite@latest <project_name> -- --template react-swc-ts
```

```
Done. Now run:
  cd myproject
  npm install
  npm run dev
```

参考：

- https://vitejs.dev/guide/#scaffolding-your-first-vite-project

## 默认打开 Chrome

打开之后，将 package.json 中 `scripts.dev` 的 `vite` 修改为 `BROWSER='google chrome' vite --open`，这样就可以在每次开发的时候默认打开 Chrome。

参考：

- https://vitejs.dev/guide/cli.html#dev-server
- https://vitejs.dev/config/server-options.html#server-open
- https://github.com/sindresorhus/open#app
