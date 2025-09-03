# Quick Nginx

> 🚀 基于 Express 的轻量级静态文件服务器，支持 API 代理转发

一个简单易用的开发工具，用于快速启动类似 nginx 的服务来验证前端构建产物，支持 API 代理转发功能。

## ✨ 特性

- 🎯 **零配置启动** - 开箱即用的静态文件服务
- 🔄 **API 代理** - 支持接口代理转发，解决开发环境跨域问题
- 🎨 **SPA 支持** - 自动处理单页应用路由回退
- ⚡ **轻量快速** - 基于 Express，启动迅速
- 🛠️ **易于配置** - 简单的配置文件，满足不同项目需求

## 📦 安装

```bash
# 克隆项目
git clone <repository-url>
cd quick-nginx

# 安装依赖
npm install
```

## 🚀 快速开始

1. **准备构建产物**
   ```bash
   # 确保你的项目根目录有 dist 文件夹（React/Vue 等项目的构建产物）
   # 或者修改 config.js 中的 projectPath 指向你的静态文件目录
   ```

2. **启动服务**
   ```bash
   npm run serve
   ```

3. **访问应用**
   ```
   打开浏览器访问: http://localhost:3001
   ```

## ⚙️ 配置

编辑 `config.js` 文件来自定义配置：

```js
const port = 3001;                              // 服务端口
const projectPath = path.join(__dirname, "./dist"); // 静态文件目录
const entryHtml = "index.html";                // 入口 HTML 文件

// API 代理配置
const proxyOptions = {
  target: "http://your-api-server.com",         // 目标服务器
  changeOrigin: true,                           // 改变请求头中的 host
  ws: true,                                     // 支持 WebSocket
  pathRewrite: {
    "^/api": "",                                // 路径重写规则
  }
};
```

### 配置示例

**指定自定义项目路径：**
```js
const projectPath = path.join("/Users/username/my-project", "dist");
```

**配置多个代理规则：**
```js
const proxyOptions = {
  target: "https://api.example.com",
  changeOrigin: true,
  pathRewrite: {
    "^/api/v1": "/v1",
    "^/api/v2": "/v2",
  }
};
```

## 🎯 使用场景

- ✅ 验证前端构建产物
- ✅ 本地开发环境 API 代理
- ✅ 快速预览静态网站
- ✅ 单页应用（SPA）本地服务
- ✅ 替代复杂的 nginx 配置

## 🔧 技术实现

基于以下技术栈：
- **Express** - Web 服务框架
- **http-proxy-middleware** - HTTP 代理中间件

核心功能：
- 静态文件服务
- API 请求代理转发
- SPA 路由回退处理
- WebSocket 代理支持

## 📝 已验证项目

- [vite-antd-pc](https://github.com/luozyiii/vite-antd-pc)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

ISC License
