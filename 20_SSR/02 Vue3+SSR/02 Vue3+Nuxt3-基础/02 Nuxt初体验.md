# 一 、Nuxt环境搭建

在开始之前，请确保您已安装推荐的设置：

 -  Node.js （最新 LTS 版本）
 -  VS Code 
	 - Volar、ESLint、Prettier

命令行工具，新建项目（hello-nuxt )

- npm create nuxt  hello-nuxt
- pnpm create nuxt hello-nuxt
- yarn create nuxt hello-nuxt

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773837037000g37ifq.png)

# 二、Nuxt目录结构

```test
my-nuxt-app/
├─ app/
│  ├─ assets/
│  ├─ components/
│  ├─ composables/
│  ├─ layouts/
│  ├─ middleware/
│  ├─ pages/
│  ├─ plugins/
│  ├─ utils/
│  ├─ app.vue
│  ├─ app.config.ts
│  └─ error.vue
├─ content/
├─ public/
├─ shared/
├─ server/
└─ nuxt.config.ts

```

这是 Nuxt 4 项目的典型目录结构解析：

- **app/**：Nuxt 4 将客户端应用的核心代码集中在此目录下，取代了 Nuxt 3 中位于根目录的多个文件夹。
	 - **assets/**：存放未经编译的静态资源，如样式文件（CSS、SCSS）、图片、字体等。这些资源会被构建工具（Vite 或 Webpack）处理。
	 - **components/**：Vue 组件目录。该目录下的组件会自动注册，无需手动导入即可在页面和布局中使用。
	 - **composables/**：Vue 组合式函数（Composables）目录。文件导出的函数会自动导入，便于在组件中复用逻辑。
	 - **layouts/**：布局组件目录。用于定义页面的通用布局，可以通过 `definePageMeta` 指定页面使用的布局。
	 - **middleware/**：路由中间件目录。可以在导航到特定路由前执行逻辑，支持全局或局部应用。
	 - **pages/**：基于文件的路由视图目录。每个 `.vue` 文件对应一个路由路径，支持动态路由和嵌套路由。
	 - **plugins/**：Vue 插件目录。在 Vue 应用初始化前运行，用于注册全局组件、注入函数或扩展 Vue 功能。
	 - **utils/**：工具函数目录（可选）。用于存放辅助函数，可通过 `#imports` 自动导入（需在 `nuxt.config.ts` 中配置）。
	 - **app.vue**：应用的根组件，是整个 Vue 应用的入口。
	 - **app.config.ts**：应用配置文件，用于定义公共运行时配置（如应用标题、主题等），可在客户端和服务器端安全地访问。
	 - **error.vue**：全局错误页面组件，用于捕获路由错误或服务器错误时的显示。
- **content/**：如果使用了 Nuxt Content 模块，该目录用于存放 Markdown、JSON、YAML 等文件，模块会将其解析为内容层。
- **public/**：静态资源目录，放在此处的文件会原样复制到构建输出目录的根路径下（如 `favicon.ico`、`robots.txt`），可通过 `/` 直接访问。
- **shared/**：自定义目录（非 Nuxt 强制目录），常用于存放客户端和服务器端共享的代码，如 TypeScript 类型定义、常量、工具函数等。
- **server/**：Nitro 服务器引擎目录，用于定义服务器端 API 和中间件。
	- 可以包含 `api/`（API 端点）、`routes/`（自定义路由）、`middleware/`（服务器中间件）等子目录，文件支持 TypeScript，自动注册为 Nitro 路由。
- **nuxt.config.ts**：Nuxt 配置文件，用于自定义 Nuxt 的行为，如模块、构建选项、运行时配置等。

# 三、应用入口（App.vue）

默认情况下，Nuxt 会将此文件视为入口点，并为应用程序的每个路由呈现其内容，常用于：

 - 定义页面布局 Layout 或 自定义布局，如：NuxtLayout
 - 定义路由的占位，如：NuxtPage
 - 编写全局样式
 - 全局监听路由 等等

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773837477000vjfpfp.png)


