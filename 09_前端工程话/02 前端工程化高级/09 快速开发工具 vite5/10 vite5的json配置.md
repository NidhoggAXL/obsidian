# 一、默认行为：开箱即用

在 Vite 项目中，你可以直接通过 `import` 语句导入 `.json` 文件。

```js
// data.json
{
  "name": "Vite",
  "version": "5.0"
}

// main.js
// 默认导入整个 JSON 对象
import data from './data.json'
console.log(data.name) // 输出: Vite

// 支持具名导入（named import），直接导入 JSON 对象的特定属性
import { version } from './data.json'
console.log(version) // 输出: 5.0
```

默认情况下，Vite 是支持具名导入（`namedExports`）的

# 二、核心配置：`json` 选项

你可以在 `vite.config.js` 文件中通过 `json` 选项来调整其行为。

```js
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  // ... 其他配置
  json: {
    // 1. 是否支持具名导入 (namedExports)
    // 默认值: true
    // 如果设为 false，则只能通过 `import data from './data.json'` 默认导入
    namedExports: true,

    // 2. 是否将 JSON 内容字符串化 (stringify)
    // 默认值: false
    // 若设置为 true，导入的 JSON 会被转为 `export default JSON.parse("...")`，
    // 这在处理大型 JSON 文件时可能会有更好的性能[reference:4][reference:5]。
    stringify: false,
  }
})
```

> [!tip] **Vite 6 的变动**：
> 从 Vite 6 开始，大于 10KB 的 JSON 导入默认会使用 `stringify` 方式

# 三、TypeScript 支持

在 TypeScript 项目中使用 JSON，需要确保 `tsconfig.json` 中启用了 `resolveJsonModule` 选项

```json
// tsconfig.json
{
  "compilerOptions": {
    "resolveJsonModule": true,
    // 为了更好的类型提示，建议开启
    "esModuleInterop": true
  }
}
```

