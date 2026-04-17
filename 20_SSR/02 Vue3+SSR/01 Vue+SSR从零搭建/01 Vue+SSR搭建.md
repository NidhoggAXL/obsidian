# 一、邂逅Vue3 + SSR

Vue除了支持开发SPA应用之外，其实也是支持开发SSR应用的。

在Vue中创建SSR应用，需要调用**createSSRApp函数**，而不是createApp

 - createApp：创建应用，直接挂载到页面上
 - createSSRApp：创建应用，是在激活的模式下挂载应用

服务端用 @vue/server-renderer 包中的 **renderToString** 来进行渲染。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17737386380007n2n2m.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773738647000utmwbr.png)

# 二、Node Server 搭建

需安装的依赖项：

 - npm i express
 - npm i –D nodemon
 - npm i -D webpack webpack-cli webpack-node-externals

nodemon:启动Node程序时并监听文件的变化，变化即刷新

webpack-node-externals：排除掉 node_modules 中所以的模块

> [!tip] 
> webpack-node-externals 这个是在node环境中需要编写的 `target: node;`，web 环境不需要编写

简单目录结构：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773748688000g73f51.png)

webpack.config.js 的配置：

```js
// webpack.config.js
const path = require("path")
//  引入webpack-node-externals模块，该模块用于将node_modules中的模块不打包进最终的bundle文件中
const nodeExternals = require("webpack-node-externals") 

module.exports = {
  target: "node",
  mode: "development",
  entry: "./src/server/index.js",
  output: {
    path: path.resolve(__dirname, "../dist"),
    filename: "server_bundle.js"
  },
  externals: [ nodeExternals() ]
}
```

package.json 的配置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773748753000jc548m.png)

# 三、Vue3 + SSR 搭建

需安装的依赖项：

 - npm i express 
 - npm i –D nodemon
 - npm i vue
 - npm i -D vue-loader
 - npm i -D babel-loader @babel/preset-env
 - npm i -D webpack webpack-cli
 - npm i -D webpack-merge webpack-node-externals

vue-loader：加载.vue文件

webpack-merge： 用来合并webpack配置

babel-loader、@babel/preset-env

- 加载JS文件，转换新语法

# 四、跨请求状态污染

在SPA中，整个生命周期中只有一个App对象实例 或 一个Router对象实例 或 一个Store对象实例都是可以的，因为每个用户在使用浏览器访问SPA应用时，应用模块都会重新初始化，这也是一种**单例模式**。

在 SSR 环境下，App应用模块通常只在服务器启动时初始化一次。同一个应用模块会在多个服务器请求之间被复用，而我们的单例状态对象也一样，也会在多个请求之间被复用，比如：

 - 当某个用户对共享的单例状态进行修改，那么这个状态可能会意外地泄露给另一个在请求的用户。
 - 我们把这种情况称为：**跨请求状态污染**。

**为了避免这种跨请求状态污染**，SSR的解决方案是：

 - 可以在每个请求中为整个应用**创建一个全新的实例**，包括后面的 router 和全局 store等实例。
 - 所以我们在创建App 或 路由 或 Store对象时都是**使用一个函数来创建**，保证每个请求都会创建一个全新的实例。
 - 这样也会有缺点：**需要消耗更多的服务器的资源**。

# 五、Vue3 SSR + Hydration

服务器端渲染页面 + 客户端激活页面，是页面有交互效果（这个过程称为：Hydration 水合）

整体目录结构：

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773760915000pxhn8x.png)


Hydration的具体步骤如下：

1. 开发一个App应用，比如App.vue

```vue
// app.vue
<script setup>
import { ref } from 'vue';

let count = ref(0)
function addCount() {
  count.value++
  // console.log("hhhhh")
}
</script>

<template>
  <div class="axl" style="border: 5px solid orange;">
    <h1>hello axl</h1>
    <h1>{{ count }}</h1>
    <button @click="e => addCount()">+1</button>
  </div>
</template>

<style scoped>

</style>
```

2. 将App.vue打包为一个客户端的client_bundle.js文件
	 - 用来激活应用，使页面有交互效果

```js
// .src/client/index.js
import { createApp } from 'vue'
import App from '../app.vue'

const app = createApp(App) 
app.mount("#app");
```

```js
// config/client.config.js
const path = require("path")
const { VueLoaderPlugin } = require("vue-loader/dist/index")

module.exports = {
  target: "web",
  mode: "development",
  entry: "./src/client/index.js",
  output: {
    path: path.resolve(__dirname, "../dist/client"),
    filename: "client_bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: "vue-loader"
      },
      {
        test: /\.js$/,
        use: [
          {
            loader: "babel-loader",
            options: {
              presets: ["@babel/preset-env"]
            }
          }
        ],
        exclude: /node_modules/
      }
    ]
  },
  plugins: [
    new VueLoaderPlugin()
  ]
}
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773760858000fngkm6.png)

```shell
npm run build:client
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773760887000rsmwhh.png)


3. 将App.vue打包为一个服务器端的server_bundle.js文件
	 - 用来在服务器端动态生成页面的HTML

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773761012000nm4t0x.png)


4. server_bundle.js 渲染的页面 + client_bundle.js 文件进行Hydration

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773761094000hny16s.png)

但是浏览器会报一个警告：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17737611340009cjg1g.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773761185000bxp0vy.png)

要就觉这个警告，可以使用 webpack 自带的一个 DefinePlugin 的插件，对 client.config.js 进行配置。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773761482000g6l9nv.png)

## webpack配置优化

将公共的配置抽取到同一个文件 comm.config.js 里面：使用 webpack-merge： 用来合并webpack配置。

```js
// comm.config.js
const { VueLoaderPlugin } = require("vue-loader/dist/index");

module.exports = {
  mode: "development",
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: "vue-loader",
      },
      {
        test: /\.js$/,
        use: [
          {
            loader: "babel-loader",
            options: {
              presets: ["@babel/preset-env"],
            },
          },
        ],
        exclude: /node_modules/,
      },
    ],
  },
  plugins: [new VueLoaderPlugin()],
  // 告诉webpack可以省略那些文件后缀
  resolve: {
    extensions: [".js", ".vue", ".json", ".css"],
  },
};

```

```js
// server.config.js
const path = require("path");
const { merge } = require("webpack-merge");
const commConfig = require("./comm.config");
//  引入webpack-node-externals模块，该模块用于将node_modules中的模块不打包进最终的bundle文件中
const nodeExternals = require("webpack-node-externals");

module.exports = merge(commConfig, {
  target: "node",
  entry: "./src/server/index.js",
  output: {
    path: path.resolve(__dirname, "../dist/server"),
    filename: "server_bundle.js",
  },
  externals: [nodeExternals()],
});

```

```js
// client.config.js
const path = require("path")
const { DefinePlugin } = require("webpack")
const { merge } = require("webpack-merge")
const commonConfig = require("./comm.config")

module.exports = merge(commonConfig, {
  target: "web",
  mode: "development",
  entry: "./src/client/index.js",
  output: {
    path: path.resolve(__dirname, "../dist/client"),
    filename: "client_bundle.js"
  },
  plugins: [
    new DefinePlugin({
      __VUE_OPTIONS_API__: JSON.stringify(false),
      __VUE_PROD_DEVTOOLS__: JSON.stringify(false),
      __VUE_PROD_HYDRATION_MISMATCH_DETAILS__: JSON.stringify(false)
    })
  ] 
})
```

# 六、Vue3 SSR + Vue Router

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773826023000zgykhi.png)


编写vue文件路由的占位：

```vue
// app.vue
<script setup>
import { ref } from "vue";

let count = ref(0);
function addCount() {
  count.value++;
  // console.log("hhhhh")
}
</script>

<template>
  <div class="axl" style="border: 5px solid orange">
    <h1>hello axl</h1>
    <h1>{{ count }}</h1>
    <button @click="(e) => addCount()">+1</button>

    <div>
      <router-link to="/">
        <button>Home页面</button>
      </router-link>
      <router-link to="/detail">
        <button>Detail页面</button>
      </router-link>
      <!-- 路由的占位 -->
      <router-view></router-view>
    </div>
  </div>
</template>

<style scoped></style>

```

创建路由和路由表：

```js
// router/index.js
const { createRouter } = require("vue-router")

const routes = [
  {
    path: "/",
    component: () => import(/* webpackChunkName: "home" */ "../views/home.vue")
  },
  {
    path: "/detail",
    component: () => import(/* webpackChunkName: "about" */ "../views/detail.vue")
  }
]

// 函数导出路由，防止跨请求污染
export default function (history) {
  return createRouter({
    history,
    routes
  })
}

```

客户端注册路由：

```js
// clent/index.js
import { createApp } from 'vue'
import App from '../app.vue'
import { createWebHistory } from 'vue-router';
import createRouter from '../router'


const app = createApp(App) 

 //  使用 serverCreateRouter 函数创建一个路由实例 
 // 该路由实例基于 createWebHistory() 创建的历史记录模式
const router = createRouter(createWebHistory())
app.use(router)

// isRead确定路由加载完成
router.isReady().then(() => {
  app.mount("#app");
})
```

服务器端监听路由接口：

```js
// server/index.js
const express = require("express");
const showHtml = require("./html");

const server = express();
// 静态资源部署
server.use(express.static("dist"));

// 匹配根路由
server.get("/", async (req, res) => {
  await showHtml(req, res);
});

// 匹配/后面的所有路由
server.get("/*any", async (req, res) => {
  await showHtml(req, res);
});

// 在8000端口开启服务器
server.listen(8000, () => {
  console.log("server is running ~");
});

```

服务器端路由的注册：

```js
// server/html.js
const { renderToString } = require("@vue/server-renderer");
//  导入 Vue Router 的 createMemoryHistory 函数 createMemoryHistory
// 是 Vue Router 提供的一个函数，用于创建内存历史记录
// 内存历史记录不依赖于浏览器的历史记录，常用于服务端渲染或测试环境
const { createMemoryHistory } = require("vue-router");

const createApp = require("../app").default;
const createRouter = require("../router/index").default;

async function showHtml(req, res) {
  let app = createApp();

  // 使用路由
  //  使用 serverCreateRouter 函数创建路由器，并传入 createMemoryHistory 作为参数 createMemoryHistory 是一个用于创建内存历史记录对象的函数，通常用于测试或非浏览器环境
  let router = createRouter(createMemoryHistory());
  app.use(router);
  //  使用路由器跳转到指定URL，如果没有提供URL则默认跳转到首页
  await router.push(req.url);
  //  等待路由器完成准备工作，确保路由导航完成后再执行后续操作
  await router.isReady();

  const htmlString = await renderToString(app);
  res.send(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
    </head>
    <body>
      <h1>vue SSR server</h1>
      <div id="app">${htmlString}</div>
      <script src="./client/client_bundle.js"></script>
    </body>
    </html>
  `);
}

module.exports = showHtml;

```

# 七、Vue3 SSR + Pinia

需再安装的依赖项：npm i pinia

注意事项：

 - 为了避免 跨请求状态污染
 - 需在每个请求中都创建一个全新pinia

定义 Store ：

```js
// store/count.js
import { defineStore } from 'pinia'

export const useCountStore = defineStore('count', {
  state: () => ({
    count: 0
  }),
  actions: {
    increment() {
      this.count++
    },
    decrement() {
      this.count--
    }
  }
})
```

vue 两个组件使用：

```vue
<script setup>
import { useCountStore } from '../store/count';
import { storeToRefs } from 'pinia';

const countStore = useCountStore()
const { count } = storeToRefs(countStore)
function addCount() {
  count.value++
  // console.log("hhhhh")
}
</script>

<template>
  <div class="axl" style="border: 8px solid blue;">
    <h1>Home</h1>
    <h1>{{ count }}</h1>
    <button @click="e => addCount()">+1</button>
  </div>
</template>

<style scoped>

</style>
```

客户端和服务器端都使用 pinia

```js
// 使用pinia
const pinia = createPinia()
app.use(pinia)
```


