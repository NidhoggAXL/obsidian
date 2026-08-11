# 一、核心访问方式：`import.meta.env`

在 Vite 项目中，**无法直接通过 Node.js 的 `process.env` 访问环境变量**，因为代码最终是在浏览器环境运行的[](https://juejin.cn/post/7319328280787337254)。Vite 提供了一个特殊的全局对象 **`import.meta.env`** 来暴露环境变量。

这些变量**在构建时会被静态替换**，因此必须使用完整的静态字符串访问，不支持动态 key 访问（如 `import.meta.env[key]`）。

**示例**：

```js
// main.js
console.log(import.meta.env.VITE_APP_TITLE) // "My App"
console.log(import.meta.env.MODE)           // "development" 或 "production"
```

# 二、内置环境变量（Built-in Variables）

Vite 默认提供了一些内置变量，无需配置即可在任何环境下使用

| 变量                         | 类型        | 说明                                                                                                                 |
| -------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------ |
| `import.meta.env.MODE`     | `string`  | 应用当前运行的**模式**（如 `development`、`production`）                                                                        |
| `import.meta.env.BASE_URL` | `string`  | 应用部署的基础 URL，由 `base` 配置项决定[](https://v5.vite.dev/guide/env-and-mode)[](https://juejin.cn/post/7319328280787337254) |
| `import.meta.env.PROD`     | `boolean` | 应用是否运行在生产环                                                                                                         |
| `import.meta.env.DEV`      | `boolean` | 应用是否运行在开发环境（与 `PROD` 相反                                                                                            |
| `import.meta.env.SSR`      | `boolean` | 应用是否运行在服务端                                                                                                         |

```js
// main.js
if (import.meta.env.DEV) {
  console.log('当前是开发环境，仅开发模式下执行')
}

// 根据环境切换 API 地址
const API_URL = import.meta.env.PROD 
  ? 'https://api.example.com' 
  : 'http://localhost:3000'
```

> [!tip] 
> 提示：import.meta.env.DEV 和 import.meta.env.PROD 在构建时会被静态替换，未使用的分支会被 tree-shaking 优化掉

# 三、自定义环境变量：`.env` 文件

Vite 使用 [dotenv](https://github.com/motdotla/dotenv) 库从项目根目录的 `.env` 文件中加载环境变量。
## 3.1 文件命名规则

Vite 支持以下 `.env` 文件，按加载优先级从低到高排列

| 文件名                 | 说明                                                   |
| ------------------- | ---------------------------------------------------- |
| `.env`              | **所有环境**都会加载（通用配置）                                   |
| `.env.local`        | **所有环境**都会加载，但**会被 Git 忽略**（本地专属配置）                  |
| `.env.[mode]`       | **仅在指定模式下**加载，如 `.env.development`、`.env.production` |
| `.env.[mode].local` | **仅在指定模式下**加载，且**会被 Git 忽略**                         |

> [!warning] **安全提示**：
> `*.local` 文件应添加到 `.gitignore` 中，避免敏感信息（如数据库密码、API 密钥）被提交到代码仓库

## 3.2 创建 `.env` 文件示

```bash
# .env（所有环境通用）
VITE_APP_NAME=MyApp
VITE_API_TIMEOUT=5000

# .env.development（开发环境）
VITE_API_BASE_URL=http://localhost:3000
VITE_DEBUG=true

# .env.production（生产环境）
VITE_API_BASE_URL=https://api.example.com
VITE_DEBUG=false
```

## 3.3 命名规则：`VITE_` 前缀

**重要**：为了防止意外将敏感环境变量暴露给客户端，**只有以 `VITE_` 为前缀的变量才会暴露到 `import.meta.env` 中**

```bash
# .env
VITE_SOME_KEY=123          # ✅ 会被暴露
DB_PASSWORD=foobar         # ❌ 不会被暴露（无 VITE_ 前缀）
```

---

```js
// main.js
console.log(import.meta.env.VITE_SOME_KEY)  // "123"
console.log(import.meta.env.DB_PASSWORD)    // undefined
```

> [!warning] **安全警告**：
> `VITE_*` 变量的值会在构建时被打包到最终的 JS 代码中，**严禁存放任何敏感信息**（如 API 密钥、数据库密码等）

## 3.4 变量值解析

所有通过 `import.meta.env` 获取的环境变量值都是**字符串类型**

```bash
# .env
VITE_API_TIMEOUT=5000
VITE_DEBUG=true
VITE_APP_VERSION=1.2.3
```

---

```js
// main.js
const timeout = Number(import.meta.env.VITE_API_TIMEOUT)  // 转为数字
const isDebug = import.meta.env.VITE_DEBUG === 'true'     // 转为布尔
```

## 3.5 变量扩展（引用其他变量）

Vite 内置了 [dotenv-expand](https://github.com/motdotla/dotenv-expand)，支持在 `.env` 文件中引用其他变量

```bash
# .env
VITE_APP_NAME=MyApp
VITE_API_BASE_URL=https://api.example.com
VITE_FULL_URL=${VITE_API_BASE_URL}/v1/${VITE_APP_NAME}
```

---

```js
// main.js
console.log(import.meta.env.VITE_FULL_URL)  
// "https://api.example.com/v1/MyApp"
```

> [!tip] 提示
> 如果要在值中使用 `$` 符号本身，需要用 `\` 转义
> ```bash
> VITE_PRICE=$100      # ❌ 会被当作变量解析
> VITE_PRICE=\$100     # ✅ 结果为 "$100"
> ```


# 四、环境加载优先级（Priority）

当多个 `.env` 文件定义了同名变量时，按以下优先级生效（从高到低）：

1. **命令行直接设置的变量**（最高优先级）

```bash
VITE_SOME_KEY=cli_value vite build
```

2. **模式特定的本地文件**：`.env.[mode].local`
    
3. **模式特定的文件**：`.env.[mode]`（如 `.env.production`）
    
4. **通用本地文件**：`.env.local`
    
5. **通用文件**：`.env`（最低优先级）

# 五、模式（Mode）与 `--mode` 参数

Vite 通过 **模式（Mode）** 来决定加载哪个 `.env.[mode]` 文件。

- **默认模式**：
    
    - `vite`（开发服务器）默认使用 `development` 模式
        
    - `vite build`（构建）默认使用 `production` 模式
        
- **自定义模式**：通过 `--mode` 参数指定

```bash
vite build --mode staging        # 加载 .env.staging
vite --mode development          # 加载 .env.development（默认）
```

**代码中获取当前模式**：

```js
console.log(import.meta.env.MODE)  // "development" 或 "production" 或 "staging"
```

# 六、在 `vite.config.js` 中使用环境变量

`vite.config.js` 运行在 Node.js 环境，因此可以直接使用 `process.env` 访问所有环境变量（不受 `VITE_` 前缀限制）

## 6.1 直接访问 `process.env`

```js
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  server: {
    port: Number(process.env.VITE_PORT) || 5173
  },
  base: process.env.VITE_BASE_URL || '/'
})
```


---

```bash
# 启动时设置
VITE_PORT=8080 VITE_BASE_URL=/my-app/ vite
```

## 6.2 使用 `loadEnv` 加载指定模式的 `.env` 文件

如果需要加载特定模式的环境变量，可以使用 Vite 提供的 `loadEnv` 工具函数

```js
// vite.config.js
import { defineConfig, loadEnv } from 'vite'

export default defineConfig(({ mode }) => {
  // 加载指定模式的环境变量，第二个参数为项目根目录
  const env = loadEnv(mode, process.cwd(), '')
  
  return {
    server: {
      port: Number(env.VITE_PORT) || 5173
    },
    define: {
      // 将环境变量注入到客户端代码
      'process.env': {
        NODE_ENV: JSON.stringify(process.env.NODE_ENV)
      }
    }
  }
})
```

`loadEnv` 的第三个参数用于指定环境变量的前缀，默认为 `'VITE_'`。如果传空字符串 `''`，则会加载所有环境变量（谨慎使用）。

# 七、TypeScript 智能提示（IntelliSense）

默认情况下，Vite 在 [`vite/client.d.ts`](https://github.com/vitejs/vite/blob/main/packages/vite/client.d.ts) 中为 `import.meta.env` 提供了类型定义。随着在 `.env[mode]` 文件中自定义了越来越多的环境变量，你可能想要在代码中获取这些以 `VITE_` 为前缀的用户自定义环境变量的 TypeScript 智能提示。

要想做到这一点，你可以在 `src` 目录下创建一个 `vite-env.d.ts` 文件，接着按下面这样增加 `ImportMetaEnv` 的定义：

```ts
// vite-env.d.ts
interface ViteTypeOptions {
  // 添加这行代码，你就可以将 ImportMetaEnv 的类型设为严格模式，
  // 这样就不允许有未知的键值了。
  // strictImportMetaEnv: unknown
}

interface ImportMetaEnv {
  readonly VITE_APP_TITLE: string
  // 更多环境变量...
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

如果你的代码依赖于浏览器环境的类型，比如 [DOM](https://github.com/microsoft/TypeScript/blob/main/src/lib/dom.generated.d.ts) 和 [WebWorker](https://github.com/microsoft/TypeScript/blob/main/src/lib/webworker.generated.d.ts)，你可以在 `tsconfig.json` 中修改 [lib](https://www.typescriptlang.org/tsconfig#lib) 字段来获取类型支持。

```ts
//tsconfig.json
{
  "lib": ["WebWorker"]
}
```

> [!warning] 导入语句会破坏类型增强
> 如果 `ImportMetaEnv` 增强不起作用，请确保在 `vite-env.d.ts` 中没有任何 `import` 语句。更多信息请参阅 [TypeScript 文档](https://www.typescriptlang.org/docs/handbook/2/modules.html#how-javascript-modules-are-defined)。

# 八、HTML 环境变量替换

Vite 还支持在 HTML 文件中替换环境变量。`import.meta.env` 中的任何属性都可以通过特殊的 `%CONST_NAME%` 语法在 HTML 文件中使用：

```html
<h1>Vite is running in %MODE%</h1>
<p>Using data from %VITE_API_URL%</p>
```

如果环境变量在 `import.meta.env` 中不存在，比如不存在的 `%NON_EXISTENT%`，则会被忽略而不被替换，这与 JS 中的 `import.meta.env.NON_EXISTENT` 不同，JS 中会被替换为 `undefined`。

正因为 Vite 被许多框架使用，它在复杂的替换（如条件替换）上故意不持任何意见。Vite 可以使用 [现有的用户插件](https://github.com/vitejs/awesome-vite#transformers) 或者一个实现了 [`transformIndexHtml` 钩子](https://cn.vite.dev/guide/api-plugin#transformindexhtml) 的自定义插件来扩展。


