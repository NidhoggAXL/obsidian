# vite插件的本质

Vite 为了将生态的扩充交给所有开发者，因此采用了插件化设计的思想，定义基础插件化协议，开发者通过遵循插件协议开发插件，一次来丰富Vite生态。


# vite-plugin-inspect

`vite-plugin-inspect` 是一个用于检查和调试 Vite 插件中间状态的工具。它主要面向 Vite 插件开发者，或是希望深入理解、优化项目构建过程的开发者。

简单来说，它的核心作用是提供一个**可视化界面**，让你能清晰地看到 Vite 构建过程中，每个文件是如何被各个插件一步步转换的。

##  主要功能与特性

- **可视化插件转换过程**：提供一个直观的 Web UI 界面，展示每个插件对每个文件的转换结果和耗时。
    
- **实时检查**：在开发模式下，可以实时查看模块的转换过程。
    
- **构建模式支持**：支持在生产构建（`vite build`）后检查转换结果。
    
- **助力插件开发与调试**：帮助插件开发者验证插件的执行顺序，调试转换过程中的问题。
    
- **零配置，开箱即用**：安装后只需在配置中添加插件即可，无需复杂设置

## 🚀 如何使用

### 1. 安装

使用你喜欢的包管理器进行安装：

```bash
npm install -D vite-plugin-inspect
# 或
yarn add -D vite-plugin-inspect
# 或
pnpm add -D vite-plugin-inspect
```

### 2. 配置

在 `vite.config.ts` 中引入并配置插件

```ts
// vite.config.ts
import { defineConfig } from 'vite';
import Inspect from 'vite-plugin-inspect';

export default defineConfig({
  plugins: [
    Inspect(), // 默认仅在开发模式启用
  ],
});
```

### 3. 查看结果

- **开发模式**：运行 `npm run dev` 后，访问 `http://localhost:5173/__inspect/` 即可查看。（端口号可能因配置而异）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1786115909000o7yry5.png)


- **构建模式**：如果需要检查构建过程，可以启用 `build` 选项

```ts
Inspect({
  build: true,
  outputDir: '.vite-inspect' // 构建结果输出目录
})
```

## 主要应用场景

- **插件开发者**：开发 Vite 插件时，用它来调试插件的转换逻辑，查看输出结果是否符合预期。
    
- **构建性能优化**：分析项目中各个插件的耗时，快速定位导致构建缓慢的“罪魁祸首”。
    
- **模块依赖分析**：查看模块之间的依赖关系和转换链路，深入理解项目的内部结构

## ⚙️ 主要配置选项

| 选项          | 类型        | 默认值               | 描述                |
| ----------- | --------- | ----------------- | ----------------- |
| `build`     | `boolean` | `false`           | 是否在构建模式下启用检查      |
| `outputDir` | `string`  | `'.vite-inspect'` | 构建模式下，检查器客户端的输出目录 |
| `dev`       | `boolean` | `true`            | 是否在开发模式下启用        |
## 版本注意事项

- `vite-plugin-inspect` **v10.x** 及以上版本需要 **Vite v6.0.1** 或更高版本。
    
- 如果你的项目使用 **Vite v2 到 v5**，请使用 **v0.8.x** 版本的插件


# 插件的配置

配置插件是在项目中使用插件的过程，非常简单：

1. **安装插件**：首先，你需要将插件包安装为项目的开发依赖 (`devDependencies`)

```bash
npm install @vitejs/plugin-vue -D
```

2. **在配置中引入**：在项目根目录的 `vite.config.js` 或 `vite.config.ts` 文件中，导入插件并将其添加到 `plugins` 数组中

```js title="vite.config.js"
// vite.config.js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue' // 导入插件

export default defineConfig({
  plugins: [
    vue(), // 使用插件
    // 可以添加更多插件...
  ],
})
```

3. **传递配置选项**：如果插件支持自定义，可以在调用时传入配置对象

```js
// vite.config.js
import { defineConfig } from 'vite'
import examplePlugin from 'vite-plugin-example'

export default defineConfig({
  plugins: [
    examplePlugin({
      // 插件的配置选项
      include: ['**/*.js'],
      option: true,
    }),
  ],
})
```

**配置小贴士：**

- **按需启用**：使用 `apply` 属性可以让插件只在开发 (`serve`) 或构建 (`build`) 阶段运行。
    
- **控制顺序**：使用 `enforce: 'pre'` 或 `enforce: 'post'` 可以强制插件在核心插件之前或之后执行。

# 插件的开发

开发插件就是创建一个具有特定钩子函数的对象。一个基础的插件结构如下

```js
// 1. 通常导出一个工厂函数，接收用户配置
export default function myPlugin(options = {}) {
  // 2. 返回一个插件对象
  return {
    // 必须：插件的唯一名称，建议以 'vite-plugin-' 开头[reference:13][reference:14]
    name: 'vite-plugin-my-example',

    // 可选：指定插件应用阶段 ('serve' | 'build')[reference:15]
    // apply: 'build',

    // 可选：控制插件执行顺序 ('pre' | 'post')[reference:16]
    // enforce: 'pre',

    // 3. 各种生命周期钩子函数
    // 通用钩子 (来自 Rollup)
    transform(code, id) {
      // 处理文件内容
    },
    // Vite 特有钩子
    config(config, env) {
      // 修改 Vite 配置
    },
    configureServer(server) {
      // 配置开发服务器
    },
    // ... 更多钩子
  }
}
```

# 开发实战与代码示例

下面通过几个例子来展示如何利用不同的钩子实现功能。

## 示例1：转换自定义文件类型

假设你想让 Vite 处理 `.myfile` 后缀的文件，并将其内容转换为 JavaScript。

```js
// vite-plugin-my-file.js
const fileRegex = /\.(myfile)$/

export default function myFilePlugin() {
  return {
    name: 'vite-plugin-my-file',
    transform(src, id) {
      // 只处理匹配的文件
      if (fileRegex.test(id)) {
        // 将文件内容转换为 JS 代码
        const code = `export default ${JSON.stringify(src)}`
        return {
          code, // 转换后的代码
          map: null, // 如有需要可提供 source map
        }
      }
    },
  }
}
```

## 示例2：注入 HTML 标签

使用 `transformIndexHtml` 钩子可以在构建时修改最终的 `index.html` 文件。

```js
// vite-plugin-inject-html.js
export default function injectHtmlPlugin() {
  return {
    name: 'vite-plugin-inject-html',
    transformIndexHtml(html) {
      // 在 </head> 标签前插入一个预连接提示
      return html.replace(
        '</head>',
        '<link rel="preconnect" href="https://api.example.com"></head>'
      )
    },
  }
}
```

## 示例3：添加自定义开发服务器中间件

通过 `configureServer` 钩子，可以为 Vite 开发服务器添加自定义路由。

```js
// vite-plugin-middleware.js
export default function middlewarePlugin() {
  return {
    name: 'vite-plugin-middleware',
    configureServer(server) {
      // 添加一个 /health 路由用于健康检查
      server.middlewares.use('/health', (req, res) => {
        res.statusCode = 200
        res.end('OK')
      })
    },
  }
}
```

## 示例4：创建虚拟模块

Vite 支持虚拟模块，即通过插件动态生成不存在的模块内容

```js
// vite-plugin-virtual.js
const virtualModuleId = 'virtual:my-env' // 解析时的 ID
const resolvedVirtualModuleId = '\0' + virtualModuleId // 解析后的 ID，Vite 内部约定

export default function virtualEnvPlugin() {
  return {
    name: 'vite-plugin-virtual-env',
    resolveId(id) {
      // 当遇到 'virtual:my-env' 时，返回一个特定的 ID
      if (id === virtualModuleId) {
        return resolvedVirtualModuleId
      }
      return null
    },
    load(id) {
      // 当加载到我们之前设定的 ID 时，动态生成内容
      if (id === resolvedVirtualModuleId) {
        return `export const mode = '${process.env.NODE_ENV}'`
      }
      return null
    },
  }
}
```

在项目中，你可以这样使用这个虚拟模块：

```js
import { mode } from 'virtual:my-env'
console.log(mode) // 输出 'development' 或 'production'
```

# 核心钩子与属性说明

一个功能完整的插件通常由 **属性** 和 **钩子** 组成。

- **插件属性**：
    
    - `name`：**必须**，唯一标识插件。
        
    - `enforce`：可选，`'pre'` 或 `'post'`，控制执行顺序。
        
    - `apply`：可选，`'serve'` 或 `'build'`，控制应用场景。
        
- **核心钩子（函数）**：
    
    - **通用钩子 (Rollup)**[](https://cloud.tencent.com.cn/developer/article/2437703?from=15425&frompage=seopage)：
        
        - `options`：在服务器启动时，替换或操作 `options` 对象。
            
        - `buildStart`：在服务器启动时，开始构建时调用。
            
        - `resolveId`：在每个传入模块请求时，自定义模块解析器。
            
        - `load`：在每个传入模块请求时，自定义模块加载器。
            
        - `transform`：在每个传入模块请求时，转换加载的模块代码。
            
        - `buildEnd` & `closeBundle`：在服务器关闭时调用。
            
    - **Vite 特有钩子**[](https://cloud.tencent.com.cn/developer/article/2437703?from=15425&frompage=seopage)：
        
        - `config`：在解析 Vite 配置前，修改配置对象。
            
        - `configResolved`：在 Vite 配置解析完成后调用。
            
        - `configureServer`：用于配置开发服务器，如添加中间件。
            
        - `transformIndexHtml`：转换 `index.html` 的内容。
            
        - `handleHotUpdate`：处理自定义的热更新逻辑。

# 命名与调试建议

- **命名规范**：Vite 插件建议以 `vite-plugin-` 为前缀，并在 `package.json` 的 `keywords` 中包含 `vite-plugin`。如果只服务于特定框架，可以加上框架名，如 `vite-plugin-vue-`。
    
- **调试利器**：强烈推荐在开发插件时使用 `vite-plugin-inspect` 工具。安装后访问 `localhost:5173/__inspect/`，可以清晰地看到每个模块被哪些插件转换过，是排查问题的神器。

总的来说，Vite 插件的开发就是围绕这些生命周期钩子来编写逻辑。

