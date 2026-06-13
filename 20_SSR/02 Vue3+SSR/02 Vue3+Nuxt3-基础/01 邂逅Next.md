# 一、什么是Nuxt？

在了解 Nuxt 之前，我们先来了解一下创建一个现代应用程序，所需的技术：

 - 支持数据双向绑定 和 组件化（ Nuxt 选择了Vue.js ）。
 - 处理客户端的导航（ Nuxt 选择了vue-router ）。
 - 支持开发中热模块替换和生产环境代码打包（ Nuxt支持webpack5和Vite ）。
 - 兼容旧版浏览器，支持最新的 JavaScript 语法转译（ Nuxt使用esbuild ）。
 - 应用程序支持开发环境服务器，也支持服务器端渲染 或 API接口开发。
 - Nuxt 使用 h3来实现部署可移植性（h3是一个极小的高性能的http框架）
	 - 如：支持在 Serverless、Workers 和 Node.js 环境中运行。

Nuxt 是一个 **直观的 Web 框架**

 - 自 2016 年 10 月以来，Nuxt专门负责集成上述所描述的事情 ，并提供前端和后端的功能。
 - Nuxt 框架可以用来快速构建下一个 Vue.js 应用程序，如支持 CSR 、SSR、SSG 渲染模式的应用等。

# 二、Nuxt3 特点

Vue技术栈：Nuxt3 是基于 Vue3 + Vue Router + Vite 等技术栈，**全程 Vue3+Vite 开发体验（Fast）**。

自动导包

 - Nuxt 会自动导入**辅助函数、组合 API和 Vue API ，无需手动导入**。
 - 基于规范的目录结构，Nuxt 还可以对自己的组件、 插件使用自动导入。

约定式路由（目录结构即路由）:Nuxt 路由基于vue-router，在 pages/ 目录中创建的每个页面，都会根据目录结构和文件名来自动生成路由

渲染模式：Nuxt 支持多种渲染模式（SSR、CSR、SSG等）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773835584000xmuh0i.png)


利于搜索引擎优化：服务器端渲染模式，不但可以提高首屏渲染速度，还利于SEO

服务器引擎

 - 在开发环境中，它使用 Rollup 和 Node.js 。
 - 在生产环境中，使用 Nitro 将您的应用程序和服务器构建到一个通用.output目录中。
	 - **Nitro服务引擎提供**了跨平台部署的支持，包括 Node、Deno、Serverless、Workers等平台上部署。

