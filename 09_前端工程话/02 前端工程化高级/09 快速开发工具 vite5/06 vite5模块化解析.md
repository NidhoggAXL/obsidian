# ⚙️ 核心配置：`resolve` 选项

`resolve` 配置项主要用于定制模块路径的解析逻辑，它有以下几个关键属性：

# alias

`alias`：设置路径别名

这是最常用的配置，用于为常用目录或特定路径创建简短的别名。它可以**简化导入路径，提高代码可维护性，并减少复杂的相对路径（如 `../../../`）**

```js
// vite.config.js
import { defineConfig } from 'vite'
import path from 'path'

export default defineConfig({
  resolve: {
    alias: {
      // 将 '@' 映射到项目根目录下的 'src' 文件夹
      '@': path.resolve(__dirname, 'src'),
      // 将 '@components' 映射到 'src/components'
      '@components': path.resolve(__dirname, 'src/components'),
      // 将 '@utils' 映射到 'src/utils'
      '@utils': path.resolve(__dirname, 'src/utils')
    }
  }
})
```

配置后，就可以在代码中这样使用：

```js
// 使用别名代替复杂的相对路径
import Button from '@components/Button'
import { formatDate } from '@utils/date'
```


# extensions

`extensions`：指定自动补全的文件扩展名

在导入语句中省略文件扩展名时，Vite 会按此列表的顺序去尝试查找文件[](https://blog.csdn.net/weixin_64684095/article/details/143205059)。这能**使导入语句更简洁**，并**控制模块解析的优先级**。

**代码示例**：

```js
// vite.config.js
export default defineConfig({
  resolve: {
    // Vite 默认支持 .mjs, .js, .ts, .jsx, .tsx, .json[reference:11]
    // 如果项目大量使用 .vue 文件，可以将其添加到列表中
    extensions: ['.mjs', '.js', '.ts', '.jsx', '.tsx', '.json', '.vue']
  }
})
```


配置后，可以省略扩展名导入：

```js
// Vite 会尝试查找 Example.vue, Example.js 等
import Example from '@/components/Example'
```

> [!tip] 
> 注意：resolve.extensions 主要影响项目源代码中的模块解析。对于 node_modules 中的依赖，其解析逻辑可能不同，有时需要通过 optimizeDeps 等配置来辅助。

# dedupe

`dedupe`：防止依赖重复加载

当项目中不同模块依赖了同一个库的**不同版本**时，`dedupe` 可以强制 Vite 只使用一个版本。这有助于**减小打包体积**并**避免因多版本共存导致的运行时冲突**。

**代码示例**：

```js
// vite.config.js
export default defineConfig({
  resolve: {
    // 强制整个项目只使用一个 React 和 ReactDOM 版本
    dedupe: ['react', 'react-dom']
  }
})
```

# conditions

 `conditions`：控制导出条件

此配置用于处理 `package.json` 中根据 `exports` 字段定义的不同环境导出。通过设置 `conditions`，你可以**告诉 Vite 在解析包时优先使用哪个版本的导出**（如 `development` 或 `production` 环境）。

**代码示例**：

```js
// vite.config.js
export default defineConfig({
  resolve: {
    // 此默认值在 Vite 5 中是内部添加的[reference:21]
    // 从 Vite 6 开始，可能需要显式配置[reference:22][reference:23]
    conditions: ['module', 'browser', 'development|production']
  }
})
```

# mainFields

`mainFields`：指定入口文件字段

当导入一个从 `node_modules` 中解析的包时，Vite 会去读取它的 `package.json`。`mainFields` 配置决定了 `package.json` 中**哪些字段会被优先用作包的入口文件**。

**代码示例**：

```js
// vite.config.js
export default defineConfig({
  resolve: {
    // 默认值通常为 ['module', 'jsnext:main', 'jsnext'] [reference:26]
    mainFields: ['module', 'main']
  }
})
```

> [!tip]
> 这对于控制是优先使用包的 ESM 版本（module 字段）还是 CommonJS 版本（main 字段）很有用。

# preserveSymlinks

`preserveSymlinks`：保留符号链接

此选项用于控制 Vite 如何处理符号链接（symlinks）。启用后（设为 `true`），Vite 会将符号链接视为文件本身，而不是解析到其真实路径。

**代码示例**：

```js
// vite.config.js
export default defineConfig({
  resolve: {
    // 默认值为 false
    preserveSymlinks: true
  }
})
```

> [!tip] 
> 这在 monorepo 等复杂项目结构中可能很有用



