# 修改输出目录-outDir

**有什么用**：  
默认情况下，执行 `vite build` 后所有产物会生成在项目根目录的 `dist` 文件夹里。当你需要将构建结果输出到其他位置（比如 `build`、`output`，或者 CI/CD 流程中指定的目录）时，通过此配置修改。

**实际效果**：  
假设你配置 `outDir: 'build-prod'`，那么构建后所有文件（HTML、JS、CSS、图片等）都会出现在 `build-prod` 文件夹中，而不是默认的 `dist`。

```js
export default defineConfig({
  build: {
    outDir: 'build-prod'
  }
})
```

# 指定静态资源子目录-assetsDir

**有什么用**：  
用于存放图片、字体、媒体文件等非 JS/CSS 静态资源的子文件夹名称。默认是 `assets`。如果你想将这些资源单独归类（如 `static` 或 `public`），可以修改此项。

**实际效果**：  
默认情况下，一张图片会被输出到 `dist/assets/logo-a1b2c3.png`。如果你设置 `assetsDir: 'images'`，则输出路径变为 `dist/images/logo-a1b2c3.png`。

```js
export default defineConfig({
  build: {
    assetsDir: 'images'   // 所有图片、字体等放入 images 文件夹
  }
})
```

# 小文件内联为Base64-assetsInlineLimit

**有什么用**：  
小于此阈值（单位：字节）的图片或静态资源会被自动转成 Base64 编码，直接内联到 JS 或 CSS 中，从而减少 HTTP 请求次数。大于此阈值的文件则单独打包成独立文件。

**实际效果**：  
默认阈值是 `4096`（即 4KB）。

- 一张 3KB 的图标：会被转成 Base64 字符串嵌入代码，浏览器无需额外请求。
    
- 一张 10KB 的大图：会被复制到 `assets` 目录，通过 `<img src="/assets/photo-xxx.png">` 单独加载。
    

如果你想调整内联大小，例如改成 10KB（10240 字节）：

**配置代码**：

```js
export default defineConfig({
  build: {
    assetsInlineLimit: 10240   // 10KB 以下内联，以上独立文件
  }
})
```


# 生成 Source Map-sourcemap

**有什么用**：  
Source Map 是一种映射文件（`.map`），用于将构建后压缩/混淆的代码映射回原始源码。开启后，浏览器开发者工具中显示的是源码而非编译后的代码，极大方便调试。

**开发环境 vs 生产环境的最佳实践**：

在**开发环境**中，我们追求极致的调试体验，因此可以直接开启 Source Map：

```js
export default defineConfig({
  build: {
    sourcemap: true   // 生成 Source Map，方便开发调试
  }
})
```

但在**生产环境**中，情况就复杂了：

- **直接设为 `false`**：完全不生成 Source Map，最安全，但线上报错只能看到压缩后的代码，难以定位问题。
    
- **直接设为 `true`**：会生成 `.map` 文件，并在 JS 文件末尾添加 `//# sourceMappingURL=` 注释。浏览器检测到该注释会自动加载 Source Map，这意味着**任何人都可以通过开发者工具查看你的原始源代码**，存在严重的安全风险。

**生产环境推荐方案：`sourcemap: 'hidden'` + Sentry 平台**

安全且高效的做法是：

1. 生成 Source Map 文件（`.map`），但不将其暴露给浏览器。
    
2. 将 Source Map 上传到 Sentry 等错误监控平台。
    
3. 上传后，从服务器上删除这些 `.map` 文件。
    

**`sourcemap: 'hidden'` 的作用**：  
`'hidden'` 是专为此场景设计的。它会生成 `.map` 文件，但**不会**在打包后的 JS 文件末尾添加 `//# sourceMappingURL=` 注释。这意味着浏览器不会主动加载 Source Map，从而保护了源码不被公开，同时 `.map` 文件可以被 Sentry 插件等工具读取并上传。

**配合 Sentry 的完整配置**：

以下是一个完整的配置示例，展示了如何将 Source Map 安全地上传到 Sentry：

1. **安装 Sentry Vite 插件**：

```shell
npm install @sentry/vite-plugin --save-dev[reference:8][reference:9]
```

2. **配置 `vite.config.js`**：

```js
// vite.config.js
import { defineConfig } from 'vite'
import { sentryVitePlugin } from '@sentry/vite-plugin'[reference:10][reference:11]

export default defineConfig({
  build: {
    // 生产环境使用 'hidden'，生成 .map 文件但不暴露给浏览器[reference:12][reference:13]
    sourcemap: 'hidden'
  },
  plugins: [
    // ... 其他插件
    // 注意：Sentry 插件应放在所有其他插件之后[reference:14]
    sentryVitePlugin({
      // 在 Sentry.io 的组织标识（slug）[reference:15]
      org: process.env.SENTRY_ORG,
      // 在 Sentry.io 的项目标识（slug）[reference:16]
      project: process.env.SENTRY_PROJECT,
      // Sentry 认证令牌[reference:17]
      // 可从 https://sentry.io/settings/account/api/auth-tokens/ 获取[reference:18]
      authToken: process.env.SENTRY_AUTH_TOKEN,
      sourcemaps: {
        // 上传 Source Map 后，从本地构建产物中删除 .map 文件[reference:19][reference:20]
        // 这是保障源码安全的关键一步
        filesToDeleteAfterUpload: ['./dist/**/*.map'],
      },
    }),
  ],
})
```

> [!tip] **提示**：
> 上述 `org`、`project` 和 `authToken` 也可以通过环境变量 `SENTRY_ORG`、`SENTRY_PROJECT` 和 `SENTRY_AUTH_TOKEN` 来设置。

3. **(可选）使用 Sentry Wizard 自动配置**：  

Sentry 官方提供了一个 Wizard 工具，可以交互式地引导你完成上述配置：

```shell
npx @sentry/wizard@latest -i sourcemaps
```

**实际效果**：

- 构建时，Vite 会在 `dist` 目录生成 `.js.map` 文件。
    
- Sentry 插件会自动将这些 `.map` 文件上传到你的 Sentry 项目。
    
- 上传成功后，插件会根据 `filesToDeleteAfterUpload` 配置自动删除本地的 `.map` 文件。
    
- 最终部署到生产环境的只有压缩后的 JS 文件，不包含 Source Map，用户无法看到源码。
    
- 当线上代码报错时，Sentry 后台会利用已上传的 Source Map 将错误栈还原为原始源码位置，方便你快速定位问题。

> [!tip] **注意**：
> Sentry Vite 插件在开发模式（`watch-mode`/`development-mode`）下不会上传 Source Map，只有运行生产构建（`npm run build`）时才会触发上传。

# 构建前清空输出目录-emptyOutDir

**有什么用**：  
决定在每次构建开始前，是否自动删除 `outDir` 目录下的所有旧文件，确保输出目录是干净的，避免残留上一次构建的无用文件。

**实际效果**：

- 默认值为 `true`：每次构建都会清空 `outDir`，保证目录整洁。
    
- 设为 `false`：保留现有文件，新文件会覆盖同名文件，但旧的无用文件会残留。
    

**配置代码**：

```js
export default defineConfig({
  build: {
    emptyOutDir: true   // 默认就是 true，无需修改
  }
})
```

# 分块大小警告阈值-chunkSizeWarningLimit

**有什么用**：  
当一个 JS 输出文件（chunk）的大小超过此阈值（单位：KB）时，Vite 会在控制台输出警告信息，提醒你可能需要做代码拆分，避免单个文件过大影响加载性能。

**实际效果**：  
默认阈值为 `500`（即 500KB）。如果你的某个依赖（如大型图表库）导致入口文件达到 600KB，构建时会显示警告。你可以调大阈值（如改为 `1000`）来消除警告，或者通过 `rollupOptions` 手动拆分代码来优化。

```js
export default defineConfig({
  build: {
    chunkSizeWarningLimit: 1000   // 改成 1MB 才警告
  }
})
```


# 代码压缩方式-minify

**有什么用**：  
控制是否压缩代码以及使用哪种压缩工具。压缩可以移除空格、注释、缩短变量名，显著减少文件体积。

**实际效果**：

- 默认值为 `'esbuild'`：使用 esbuild 进行压缩，速度极快，是 Vite 的默认推荐。
    
- 设为 `'terser'`：使用 Terser 压缩，压缩率通常比 esbuild 略高（尤其是针对 ES5 兼容场景），但速度慢很多。
    
- 设为 `false`：完全禁用压缩，产物保留原始格式，适合调试或某些特殊场景。
    

绝大多数项目保持默认 `'esbuild'` 即可，因为它的压缩效果已经足够好，且速度优势明显。

```js
export default defineConfig({
  build: {
    minify: 'esbuild'   // 默认值，保持即可
    // 如需极致压缩体积可改为 'terser'，但构建时间会变长
  }
})
```

# 最强大的扩展：底层 Rollup 配置-rollupOptions

**有什么用**：  
Vite 底层使用 Rollup 进行打包。`rollupOptions` 允许你直接传递 Rollup 的原生配置项，以实现更精细的控制，比如：

- **多入口打包**：适用于多页应用（MPA），指定多个 HTML 入口。
    
- **外部化依赖**：将某些大库（如 Vue、React）标记为外部依赖，不打包进产物，而是通过 CDN 引入。
    
- **手动代码拆分（静态分包)**：将公共库单独拆分为独立的 vendor 文件。
	
- **动态加载（懒加载）**：使用import函数来进行懒加载。

```js
export default defineConfig({
  build: {
    rollupOptions: {
      // 多入口配置：指定多个 HTML 作为入口
      input: {
        main: 'index.html',       // 访问 / 或 /main.html
        admin: 'admin.html'       // 访问 /admin.html
      },
      // 外部化依赖：将 vue 排除，不打包进产物
      external: ['vue'],
      // 手动拆分为 vendor 和业务代码
      output: {
        manualChunks: {
          vendor: ['vue', 'vue-router', 'axios']   // 这些库单独打包为 vendor.[hash].js
        }
      }
    }
  }
})
```


> [!tip] **注意**：
> 如果使用了 `external`，你需要确保在 HTML 中通过 CDN 或 `<script>` 标签提前加载这些依赖。


## `manualChunks`的函数用法

除了使用对象来指定分包规则外，`manualChunks` 还支持传入一个**函数**，这提供了极大的灵活性，可以根据模块的路径、名称等动态决定它属于哪个 chunk。

**函数签名**：

```js
manualChunks(id: string, { getModuleInfo, getModuleIds }) => string | void
```

**参数说明**：

- **`id`**：当前模块的绝对路径（字符串），你可以通过它来判断模块的来源，例如是否来自 `node_modules`，或者是否包含特定路径。
    
- **`getModuleInfo`**：一个工具函数，可以获取其他模块的信息，用于更复杂的依赖分析。
    
- **`getModuleIds`**：一个工具函数，可以获取所有模块的 ID 列表。
    

**返回值**：

- 返回一个**字符串**：这个字符串就是该模块所属 chunk 的名称。所有返回相同字符串的模块会被打包到同一个文件中。
    
- 返回 `undefined` 或 `void`：表示不对此模块进行特殊处理，交由 Rollup 的默认拆分逻辑处理。

### 场景一：将所有第三方依赖打包到一个文件中

这是最简单的函数用法，将所有来自 `node_modules` 的模块都归入 `vendor` 这个 chunk。

```js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          if (id.includes('node_modules')) {
            return 'vendor'   // 所有第三方依赖都进入 vendor.[hash].js
          }
        }
      }
    }
  }
})
```

**实际效果**：  
构建后，所有第三方库（Vue、React、axios、lodash 等）都会被合并到一个 `vendor.[hash].js` 文件中，业务代码则保留在 `index.[hash].js` 或其他入口文件中。

### 场景二：按包名分别打包（npm 项目）

这种策略让每个主要的第三方库都拥有独立的 chunk，可以利用浏览器并行加载，也方便缓存——只有发生变更的库才会更新哈希值

```js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          if (id.includes('node_modules')) {
            // 从路径中提取包名：'node_modules/axios/index.js' -> 'axios'
            const pkgName = id.toString().split('node_modules/')[1].split('/')[0]
            return pkgName   // 每个包单独打包：axios.[hash].js、lodash.[hash].js 等
          }
        }
      }
    }
  }
})
```

**实际效果**：

- `axios` 被打包为 `axios.[hash].js`
    
- `lodash` 被打包为 `lodash.[hash].js`
    
- `element-plus` 被打包为 `element-plus.[hash].js`
    
- 依此类推，每个 `node_modules` 下的包都独立成一个文件。

> [!tip] **注意**：
> 如果项目使用 **pnpm**，由于它的依赖组织结构不同（如 `node_modules/.pnpm/`），上述简单的 `split` 逻辑可能不生效。此时可以用正则来适配两种包管理：
> ```js
> manualChunks(id) {
  // 匹配 npm 格式：node_modules/axios/
  const npmMatch = id.toString().match(/node_modules\/([^/]+)\//)
  if (npmMatch) return npmMatch[1]
  // 匹配 pnpm 格式：node_modules/.pnpm/axios@1.0.0/node_modules/axios/
  const pnpmMatch = id.toString().match(/node_modules\/(@[^/]+\/[^/]+|[^/]+)\//)
  if (pnpmMatch) return pnpmMatch[1]
 }
> ```

### 场景三：指定部分依赖单独打包，其余归入 vendor

这种策略将常用的、体积大的库（如 Vue 全家桶、UI 库）单独拆分，其余小库合并到 `vendor` 中，在拆分粒度与请求数量之间取得平衡

```js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          // 指定哪些库需要单独打包
          const specialLibraries = {
            'vue': 'vue',
            'vue-router': 'vue',
            'pinia': 'vue',
            'element-plus': 'element-plus',
            'echarts': 'echarts'
          }

          if (id.includes('node_modules')) {
            // 遍历 specialLibraries，检查当前模块是否匹配某个库
            for (const [libName, chunkName] of Object.entries(specialLibraries)) {
              if (id.includes(libName)) {
                return chunkName   // 匹配到则进入对应的 chunk
              }
            }
            // 未匹配到任何特殊库，归入 vendor
            return 'vendor'
          }
        }
      }
    }
  }
})
```

**实际效果**：

- `vue`、`vue-router`、`pinia` 合并到 `vue.[hash].js`
    
- `element-plus` 单独打包为 `element-plus.[hash].js`
    
- `echarts` 单独打包为 `echarts.[hash].js`
    
- 其他所有第三方依赖（如 `lodash`、`axios`、`dayjs` 等）合并到 `vendor.[hash].js`

### 场景四：按业务目录拆分（文件夹分包）

适用于大型项目，希望将不同业务模块（如 `admin`、`user`、`dashboard`）的代码拆分成独立的 chunk，实现按需加载。

```js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          // 根据源码路径进行分组
          if (id.includes('src/modules/admin')) {
            return 'admin'
          } else if (id.includes('src/modules/user')) {
            return 'user'
          } else if (id.includes('src/modules/dashboard')) {
            return 'dashboard'
          } else if (id.includes('node_modules')) {
            return 'vendor'   // 第三方依赖统一归入 vendor
          }
          // 其他代码走默认逻辑
        }
      }
    }
  }
})
```

### 场景五：综合策略（按包名拆分 + 按目录拆分）

这是最复杂的场景，同时处理第三方依赖和业务代码，实现精细化的分包控制。

```js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          // 1. 第三方依赖：按包名分别打包
          if (id.includes('node_modules')) {
            const pkgName = id.toString().split('node_modules/')[1].split('/')[0]
            // 对某些大型库特殊处理，合并相关包
            if (['vue', 'vue-router', 'pinia'].includes(pkgName)) {
              return 'vue-vendor'
            }
            if (['element-plus', '@element-plus/icons-vue'].includes(pkgName)) {
              return 'ui-vendor'
            }
            return pkgName
          }

          // 2. 业务代码：按模块目录拆分
          if (id.includes('src/pages/admin')) {
            return 'admin'
          }
          if (id.includes('src/pages/dashboard')) {
            return 'dashboard'
          }
          if (id.includes('src/components/shared')) {
            return 'shared'
          }

          // 3. 其他代码走默认逻辑
        }
      }
    }
  }
})
```

**实际效果**：

- Vue 全家桶 → `vue-vendor.[hash].js`
    
- Element Plus 及图标库 → `ui-vendor.[hash].js`
    
- 其他第三方库（如 `axios`、`lodash`）→ 各自独立的 `axios.[hash].js`、`lodash.[hash].js`
    
- 后台管理页面代码 → `admin.[hash].js`
    
- 仪表盘页面代码 → `dashboard.[hash].js`
    
- 共享组件 → `shared.[hash].js`


### 重要注意事项

1. **函数返回 `undefined` 的情况**：如果某个模块不匹配任何规则，函数返回 `undefined`，Rollup 会使用其默认的拆分逻辑来处理该模块。
    
2. **与 `inlineDynamicImports` 冲突**：如果启用了 `output.inlineDynamicImports`（将所有动态导入内联），则 `manualChunks` 会失效并报错。
    
3. **调试技巧**：在函数内部使用 `console.log(id)` 可以打印所有模块的路径，帮助你分析依赖结构，从而制定更精准的拆分规则。
    
4. **性能考量**：拆分的 chunk 数量并非越多越好。过多的 chunk 会增加 HTTP 请求数量，影响首屏加载速度。通常建议将**长期不变的大型依赖**（如 Vue、UI 库）单独拆分以便缓存，而将**频繁变动的业务代码**按路由或模块拆分以实现按需加载。


