# 一、集成方案

Element Plus UI组件库

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1761803826000k0oobr.png)

集成方案： 

- 安装：https://element-plus.gitee.io/zh-CN/guide/installation.html 
- 导入：https://element-plus.gitee.io/zh-CN/guide/quickstart.html

# 二、按需引入TS配置

在按需引入的时候，TS的提示不是很好，要进行配置：把那两个插件放入到 TS 检测的文件中。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1761803919000sioite.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17618039690000brt02.png)

# 三、Icon的集成

Element-Plus的Icon组件文档中有这么一句话[说明](https://element-plus.org/zh-CN/component/icon)：如果你想像用例一样**直接使用**，你需要<mark class="hltr-cyan">全局注册组件</mark>，才能够直接在项目里使用。

在使用Element-Plus库的Icon组件的时候，如果要和它的例子一样使用 Icon 组件的话，必须全局注册，按需引入的话会有问题。

## 3.1 全局注册

为了代码的逻辑性强，会在 src 下面创建一个 global 文件，里面存放 `regitser-icons.ts` 文件，在里面编写[[04 Vue中安装插件的方式|Vue的插件]]：

```ts
import type { App } from 'vue'
import * as ElementPlusIconsVue from "@element-plus/icons-vue"

function RefisterIcons(app: App<Element>) {
  for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
    app.component(key, component)
  }
}

export default RefisterIcons

```

再在 main.ts 文件里面使用插件：

```ts
import { createApp } from "vue"
//引入自定义插件
import RegisterIcons from '@/global/register-icons'

import "normalize.css"
import "./styles/index.less"

import router from "./router/index"
import pinia from "./stores"

import App from "./App.vue"

createApp(App).use(router).use(pinia).use(RegisterIcons).mount("#app")

```

