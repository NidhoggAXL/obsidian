# 一、创建方式

创建React项目的命令如下： 

- 注意：项目名称不能包含大写字母 
- 另外还有更多创建项目的方式，可以参考GitHub的readme

```bash
npm create vite@latest my-app -- --template react
```

创建完成后，进入对应的目录，就可以将项目跑起来：

```bash
cd my-app
npm install
npm run dev
```

# 二、目录结构

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755052817000etog1m.png)

```
├── node_modules/      # 项目依赖库
├── public/            # 静态资源目录
├── src/               # 核心源代码目录
├── .gitignore         # Git 忽略规则配置
├── eslint.config.js   # ESLint 静态检查配置
├── index.html         # 应用入口 HTML
├── package-lock.json  # 依赖树锁定文件
├── package.json       # 项目配置和依赖管理
├── README.md          # 项目说明文档
└── vite.config.js     # Vite 构建工具配置
```

## 2.1 eslint.config.js

这个 ESLint 配置文件使用了 ESLint 的新扁平配置格式（Flat Config），专门为现代 JavaScript/React 项目设计。

### 2.1.1 模块导入

```js
// eslint.config.js
import js from '@eslint/js'  // ESLint 核心规则集
import globals from 'globals' // 环境全局变量定义
import reactHooks from 'eslint-plugin-react-hooks' // React Hooks 规则
import reactRefresh from 'eslint-plugin-react-refresh' // React Fast Refresh 规则
import { defineConfig, globalIgnores } from 'eslint/config' // 配置工具
```

### 2.1.2 全局忽略配置

```js
// eslint.config.js
globalIgnores(['dist'])
```

- **作用**：全局忽略指定目录/文件
    
- `dist`：构建输出目录，不需要进行代码检查
    
- 等同于传统配置中的 `ignorePatterns: ['dist']`

### 2.1.3 主配置对象

```js
// eslint.config.js
{
  files: ['**/*.{js,jsx}'], // 应用此配置的文件类型
  extends: [ // 继承的规则集
    js.configs.recommended, // ESLint 官方推荐规则
    reactHooks.configs['recommended-latest'], // React Hooks 最新推荐规则
    reactRefresh.configs.vite, // Vite 专用的 React Fast Refresh 规则
  ],
  languageOptions: { // 语言环境配置
    ecmaVersion: 2020, // JavaScript 语法版本 (ES2020)
    globals: globals.browser, // 浏览器环境全局变量 (window, document等)
    parserOptions: { // 解析器选项
      ecmaVersion: 'latest', // 使用最新 ECMAScript 特性
      ecmaFeatures: { jsx: true }, // 启用 JSX 支持
      sourceType: 'module', // 使用 ES 模块
    },
  },
  rules: { // 自定义规则
    'no-unused-vars': ['error', { 
      varsIgnorePattern: '^[A-Z_]' // 忽略大写字母或下划线开头的变量
    }],
  },
}
```

#### A. 继承的规则集 (`extends`)

| 规则集                                        | 作用             | 包含的重要规则                                                     |
| ------------------------------------------ | -------------- | ----------------------------------------------------------- |
| `js.configs.recommended`                   | ESLint 核心推荐规则  | `no-unused-vars`, `no-redeclare` 等                          |
| `reactHooks.configs['recommended-latest']` | React Hooks 规范 | `react-hooks/rules-of-hooks`, `react-hooks/exhaustive-deps` |
| `reactRefresh.configs.vite`                | Vite 热更新支持     | `react-refresh/only-export-components`                      |
#### B. 语言选项 (`languageOptions`)

1. **`ecmaVersion: 2020`**
    
    - 支持 ES2020 特性：可选链(`?.`)、空值合并(`??`)、动态导入等
        
2. **`globals: globals.browser`**
    
    - 自动识别浏览器全局对象：`window`, `document`, `fetch` 等
        
    - 避免未定义变量错误
        
3. **`parserOptions`**
    
    - `ecmaVersion: 'latest'`: 支持所有最新 JS 特性
        
    - `jsx: true`: 启用 JSX 语法解析
        
    - `sourceType: 'module'`: 使用 ES6 模块系统

#### C. 自定义规则 (`rules`)

```js
'no-unused-vars': ['error', { 
  varsIgnorePattern: '^[A-Z_]' 
}]
```

- **规则**：禁止未使用变量
    
- **级别**：`error`（编译失败）
    
- **例外**：忽略以大写字母或下划线开头的变量
    
    - 常见用例：`const API_URL = ...` 或 `const _internalVar = ...`
        
    - 避免对常量或私有变量报错


### 2.1.4 配置文件工作原理

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755053448000tukle2.png)

**为什么这样配置？**

1. **Vite 优化**  
    `reactRefresh.configs.vite` 确保组件符合 Vite 的热更新要求
    
2. **React Hooks 安全**  
    `exhaustive-deps` 规则强制 useEffect 等 Hook 声明完整依赖
    
3. **现代 JS 支持**  
    `ecmaVersion: 'latest'` 允许使用最新 JS 特性
    
4. **实用例外**  
    忽略常量未使用警告，减少无效报错


```jsx
// 会触发错误（未使用变量）
function MyComponent() {
  const unused = 'test'; // 错误! 'unused' 已定义但未使用
  
  return <div>Hello</div>;
}

// 不会触发错误（符合例外规则）
function ConstantsDemo() {
  const API_ENDPOINT = 'https://api.example.com'; // 允许: 大写开头
  
  return <div>Connect to {API_ENDPOINT}</div>;
}
```



## 2.2 主要文件结构

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17550690070001fdnb9.png)

上面的导出也可以是

```jsx
import ReactDOM form 'react-dom/client'
import App from './App.jsx'

ReactDOM.createRoot(document.getElementByid('root')).render(<App />)
```

为什么可以这样呢?**其实是进行了多次导出的**

```js
export function createRoot(){}

export default ReactDOM;
```

