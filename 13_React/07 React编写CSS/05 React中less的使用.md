# 一、vite构建工具

## 1. 安装必要依赖

```bash
npm install less less-loader -D
# 或
yarn add less less-loader -D
# 或
pnpm add less less-loader -D
```

##  2. 配置 vite.config.js

在项目根目录修改 `vite.config.js` 文件：

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  css: {
    preprocessorOptions: {
      less: {
        // 可选：全局变量/混入（mixin）配置
        additionalData: `@import "@/styles/vars.less";`,
        math: "always", // 启用 Less 4.0 数学计算
        javascriptEnabled: true, // 允许内联 JavaScript
      }
    }
  },
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src') // 配置别名（确保已安装 path 模块）
    }
  }
})
```

## 3. 创建示例 Less 文件

在 `src` 目录下创建样式文件：

```less
// src/styles/vars.less
@primary-color: #1890ff;
@text-color: #333;
```

```less
// src/App.less
.container {
  background: lighten(@primary-color, 40%);
  padding: 20px;

  h1 {
    color: @primary-color;
    &:hover {
      color: darken(@primary-color, 10%);
    }
  }

  // 使用嵌套语法
  .content {
    font-size: 16px;
    color: @text-color;
  }
}
```

## 4. 在组件中使用

```jsx
// src/App.jsx
import './App.less' // 直接导入 less 文件

function App() {
  return (
    <div className="container">
      <h1>Vite + Less 示例</h1>
      <div className="content">
        <p>成功配置了 Less 预处理器！</p>
      </div>
    </div>
  )
}

export default App
```

## 5. CSS module (可选)

创建模块化 Less 文件 (`*.module.less`)：

```less
// src/components/Button.module.less
@btn-color: #ff4d4f;

.btn {
  background: @btn-color;
  border-radius: 4px;

  &:hover {
    background: lighten(@btn-color, 10%);
  }
}
```

在组件中使用模块化样式：

```jsx
// src/components/Button.jsx
import styles from './Button.module.less'

export default function Button() {
  return (
    <button className={styles.btn}>
      Less 模块化按钮
    </button>
  )
}
```

## 6. 常见问题解决

**问题：** 报错 `Inline JavaScript is not enabled`  
**解决：** 在 `vite.config.js` 中添加：

```js
preprocessorOptions: {
  less: {
    javascriptEnabled: true
  }
}
```

**问题：** 全局变量不生效  
**解决：** 确保配置中正确设置了 `additionalData`：

```js
additionalData: `@import "@/styles/global.less";`
```

## 最终项目结构

```text
my-vite-app/
├── src/
│   ├── styles/
│   │   ├── vars.less         # 全局变量
│   │   └── mixins.less       # 全局混入
│   ├── App.less              # 全局样式
│   ├── App.jsx
│   └── components/
│       ├── Button.module.less # 模块化样式
│       └── Button.jsx
├── vite.config.js
└── package.json
```

## 特性说明

1. **原生支持**：Vite 内置 Less 支持，无需额外插件
    
2. **热更新**：样式修改即时生效
    
3. **作用域隔离**：通过 `*.module.less` 实现组件级样式封装
    
4. **完整特性**：支持变量、嵌套、混入、函数等所有 Less 功能
    

> [!tip] 提示：对于大型项目，建议：
> 
> 1. 在 `src/styles/` 目录集中管理全局变量和混入
>     
> 2. 使用 CSS Modules 避免样式冲突
>     
> 3. 通过 `alias` 配置路径别名简化导入


# 二、Webpack构建工具

因为 [Crate React App](https://react.dev/blog/2025/02/14/sunsetting-create-react-app?utm_source=tldrnewsletter)被弃用，webpack如果构建出来的React项目想要使用less，那么就需要使用 [craco](https://github.com/dilanx/craco/issues/707) 对Webpack配置

> [!warning] 具体如何配置，需要查询网络

