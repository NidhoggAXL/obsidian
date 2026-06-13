# 一、Next环境搭建

在开始之前，请确保你的系统满足以下要求：

- Node.js 20.9 或更高版本。
 - macOS、Windows（包括 WSL）或 Linux。

创建一个项目，项目名不支持大写

 - 方式一： npx create-next-app@latest --typescript
 - 方式二： yarn create next-app --typescript
 - 方式三： pnpm create next-app –typescript
 - 方式四(推荐)：npm i create-next-app@latest –g && create-next-app

运行项目

 - npm run dev
 - yarn dev
 - pnpm dev

# 二、Next.js目录结构

```test
my-nextjs-app/
├── app/                          # App Router 应用目录
│   ├── favicon.ico               # 网站图标
│   ├── globals.css               # 全局样式（Tailwind 或自定义）
│   ├── layout.tsx                # 根布局组件，定义页面共享结构（如 <html>、<body>）
│   ├── page.tsx                  # 根路由页面，对应路径 /
│   └── ...
├── components/                   # 自定义组件（非 Next.js 强制，但常见）
├── lib/                          # 工具函数、数据获取逻辑等
├── public/                       # 静态资源目录（图片、字体等，通过根路径直接访问）
│   ├── next.svg
│   └── vercel.svg
├── .env.local                    # 本地环境变量（不提交至 Git）
├── .gitignore
├── AGENTS.md                     # Next.js 16 新增，为 AI 编程助手提供的项目上下文说明
├── next-env.d.ts                 # Next.js 的 TypeScript 类型定义
├── next.config.ts                # Next.js 配置文件（支持 TypeScript）
├── package.json
├── postcss.config.mjs            # PostCSS 配置（若使用 Tailwind 等）
├── README.md
├── tailwind.config.ts            # Tailwind CSS 配置文件（若选用）
├── tsconfig.json                 # TypeScript 配置
└── ...其他配置文件
```

# 三、page.tsx-页面内容

- **作用**：定义一个具体的路由页面，即用户访问某个路径时实际看到的内容。
    
- **文件位置**：放在 `app` 目录下的任意文件夹中，文件名必须是 `page.tsx`（或 `.js`、`.jsx`）。
    
- **行为**：该文件导出的 React 组件会被 Next.js 自动映射为对应的路由。
    
    - 例如：`app/about/page.tsx` → `/about` 路由。
        
- **特点**：
    
    - 每个 `page.tsx` 都继承其所在文件夹（及父级文件夹）中的 `layout.tsx`。
        
    - 可以有自己独立的 `generateMetadata`、`generateStaticParams` 等数据获取方法。

```tsx
// app/about/page.tsx
export default function AboutPage() {
  return <h1>关于我们</h1>;
}
```

# 三、布局组件(layout.tsx)

- **作用**：定义**共享的 UI 结构**，包裹所有子页面和子布局。
    
- **文件位置**：同样放在 `app` 的任意文件夹中，文件名为 `layout.tsx`。
    
- **行为**：
    
    - 必须导出默认 React 组件，并接收一个 `children` prop，用于渲染其子内容（子 page 或子 layout）。
        
    - **嵌套布局**：文件夹层级越深，布局会嵌套越深，形成布局树。
        
    - 根布局（`app/layout.tsx`）是必需的，它包裹整个应用，通常包含 `<html>`、`<body>` 等全局结构。
        
- **特点**：
    
    - 布局在导航时**不会重新渲染**（除非通过路由分组或其他方式强制刷新），因此适合放置导航栏、侧边栏等需要保持状态的组件。
        
    - 可以访问路由参数（通过 `params` prop）。

```tsx
/** * 导入Next.js的Metadata类型，用于定义页面元数据 */
import type { Metadata } from "next";
/** * 从next/font/google导入Geist和Geist_Mono字体 */
import { Geist, Geist_Mono } from "next/font/google";
/** * 导入全局样式文件 */
import "./globals.css";

/** * 配置Geist Sans字体 * 设置变量名为"--font-geist-sans" * 只加载拉丁字母字符子集 */
const geistSans = Geist({
  variable: "--font-geist-sans",
  subsets: ["latin"],
});

/** * 配置Geist Mono字体 * 设置变量名为"--font-geist-mono" * 只加载拉丁字母字符子集 */
const geistMono = Geist_Mono({
  variable: "--font-geist-mono",
  subsets: ["latin"],
});

export const metadata: Metadata = {
  /** * 定义页面元数据 * 设置页面标题和描述 */
  title: "next demo",
  description: "网易云项目",
};

/**
概述：这是一个React组件，用于定义应用程序的根布局结构。它包裹整个应用程序的内容，并设置了基本的HTML结构，包括语言属性和字体变量。
参数：children: React.ReactNode - 包含应用程序的主要内容，将被渲染在布局的body部分
返回值：返回一个包含HTML和body标签的React元素，设置了语言属性、字体变量类名，并将children内容渲染在body中。
 */
export default function RootLayout({children,}: Readonly<{children: React.ReactNode;}>) {
  return (
    <html
      lang="en" //  设置 HTML 的语言属性为英语
      //  设置字体和样式类
      className={`${geistSans.variable} ${geistMono.variable} h-full antialiased`}
    >
      {/* 设置最小高度为全屏并使用 flex 布局  */}
      <body className="min-h-full flex flex-col">
        <header>全局导航</header>
        {children}
        <footer>尾部内容</footer>
      </body>
    </html>
  );
}

```


