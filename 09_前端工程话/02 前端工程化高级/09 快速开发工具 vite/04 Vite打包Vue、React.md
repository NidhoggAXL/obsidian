# 一、Vite对vue的支持

vite对vue提供第一优先级支持：

 - Vue 3 单文件组件支持：@vitejs/plugin-vue
 - Vue 3 JSX 支持：@vitejs/plugin-vue-jsx
 - Vue 2 支持：underfin/vite-plugin-vue2

安装支持vue的插件：

```shell
npm install @vitejs/plugin-vue -D
```

在vite.config.js中配置插件：可以使用 vite 提供的 defineConfig 来给更好的提示

```js
// vite.config.js
//  导入 Vite 的 defineConfig 函数，该函数用于定义 Vite 的配置对象
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

export default defineConfig({
  plugins: [vue()]
})
```

# 二、Vite对react的支持

.jsx 和 .tsx 文件同样开箱即用，它们也是通过 ESBuild来完成的编译：

 - 所以我们只需要直接编写react的代码即可；
 - 注意：在index.html加载main.js时，我们需要将main.js的后缀，修改为 main.jsx 作为后缀名；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17735871510006g44rl.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773587156000mzbsgy.png)

