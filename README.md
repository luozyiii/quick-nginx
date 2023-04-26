# quick-nginx【试验性项目】

基于 web 的开发流程，快速启动一个`类似 nginx` 服务验证打包的 dist。

### 背景

> http-serve 只是可以快速帮我们启动服务，并没有实现代理转发接口；
> nginx 可以实现，有一定的学习成本；希望通过 node 简单实现一下。

### 命令

```bash
# 根目录有 react vue 项目的构建产物dist
# 启动
npm run serve
```

## express + http-proxy-middleware 实现

```js
// app.js
const path = require("path");
const express = require("express");
const { createProxyMiddleware } = require("http-proxy-middleware");
const { port, projectPath, entryHtml, proxyOptions } = require("./config");

const app = express();

// 根路由
app.get("/", (req, res) => {
  res.sendFile(path.join(projectPath, entryHtml));
});

// 代理转发路由
const apiProxy = createProxyMiddleware(proxyOptions);
app.use("/api", apiProxy);

// 静态资源路由
const staticMiddleware = express.static(projectPath);
app.use(staticMiddleware);

// 未匹配的路由
app.get("*", (req, res) => {
  res.sendFile(path.join(projectPath, entryHtml));
});

app.listen(port, () => {
  console.log(`服务已启动，http://localhost:${port}`);
});
```

```js
// config.js
// 项目地址和代理转发：根据项目实际情况配置
const path = require("path");

const port = 3001; // 端口

// 当前项目地址
const projectPath = path.join(__dirname, "./dist");
const entryHtml = "index.html"; // 入口html

// 代理
const proxyOptions = {
  // target: "https://api.com", // target host
  target: "http://xxx.com/api",
  changeOrigin: true, // needed for virtual hosted sites
  ws: true, // proxy websockets
  pathRewrite: {
    "^/api": "",
    // "^/api/remove/path": "/path",
  },
  router: {
    "dev.localhost:3000": "http://localhost:8000",
  },
};

module.exports = {
  port,
  projectPath,
  entryHtml,
  proxyOptions,
};
```

- 指定本地目录，修改 projectPath 即可。

```js
const projectPath = path.join(
  "/Users/luozhiyi/Work/github/vite-antd-pc",
  "dist"
);
```

### 使用过的项目

- [vite-antd-pc](https://github.com/luozyiii/vite-antd-pc)
