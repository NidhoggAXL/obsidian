# 一、邂逅React+SSR

React和Vue一样，除了支持开发SPA应用之外，其实也是支持开发SSR应用的。

在React中创建SSR应用，需要**调用 ReactDOM.hydrateRoot 函数，而不是ReactDOM.createRoot**

 - createRoot ：创建一个Root，接着调用其 render 函数将App直接过载到页面上
 - hydrateRoot ：创建水合Root ，是在激活的模式下渲染 App

服务端可用 ReactDOM.renderToString 来进行渲染。

```ts
// src/client/index.ts
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from '../app'
// 水合 hydration
ReactDOM.hydrateRoot(document.getElementById("root"), <App/>)
```


# 二、Node Server 搭建

需安装的依赖项：

 - npm i express 
 - npm i -D nodemon
 - npm i -D webpack webpack-cli webpack-node-externals

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774429482000718fdk.png)

# 三、React18 SSR+Hydration

安装的依赖项同前面一样

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774429523000cuu9nh.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17744295360000ult0s.png)


# 四、React18 SSR+Router

安装的依赖项同前面一样，还需增加 `npm i react-router-dom` ( 默认会自动安装 react-router )

1. 编写路由映射表

```js
// src/router/index.js
import React from 'react'
import About from '../pages/about'
import Home from '../pages/home'
const router = [
  {
    path: "/",
    element: <Home />
  },
  {
    path: "/about",
    element: <About />
  }
]

export default router
```

2. 入口组件使用路由

```jsx
import { useState } from "react";
import React from "react";
import { Link, useRoutes } from "react-router-dom";

import routes from "./router/index";

const App = function () {
  const [counter, setCounter] = useState(100);
  function addCounter() {
    setCounter(counter + 1);
  }
  return (
    <div>
      <h1>React App</h1>
      <div>{counter}</div>
      <button onClick={addCounter}>+1</button>
      <div>
        <Link to="/">
          <button>home</button>
        </Link>
        <Link to="/about">
          <button>about</button>
        </Link>
        {useRoutes(routes)}
      </div>
    </div>
  );
};

export default App;
```

3. 客户端使用浏览器路由，使用 BrowserRouter 包裹

```js
// src/client/index.js
import React from 'react'
import ReactDOM from 'react-dom/client'
import  { BrowserRouter} from 'react-router-dom'
import App from '../app'
// 水合 hydration
ReactDOM.hydrateRoot(document.getElementById("root"),
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

4. 服务器端使用静态路由，使用 StaticRouter 包裹

```js
// src/server/index.jsx
import ReactDOM from "react-dom/server";
import React from "react";
import { StaticRouter } from "react-router-dom";

const express = require("express");
import App from "../app";

const server = express();
server.use(express.static("dist"));
// 匹配/路径和所有其他路径
server.get("/{*splat}", (req, res) => {
  // 将React组件渲染成HTML字符串
  const htmlString = ReactDOM.renderToString(
    <StaticRouter location={req.url}>
      <App />
    </StaticRouter>,
  );
  res.send(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
    </head>
    <body>
      <div id="root">${htmlString}</div>
      <script src="client/client_bundle.js"></script>
    </body>
    </html>
  `);
});

server.listen(3000, () => {
  console.log("server is running on port 3000");
});

```

# 五、React18 SSR+Redux

安装的依赖项同前面一样，还需增加

 - npm i react-redux @reduxjs/toolkit
 - npm i axios

Redux Toolkit 是官方推荐的编写 Redux 逻辑的方法。

 - 以前在使用redux时，通常会将redux代码拆分在多个模块中，每个模块需包含多个文件，如：constants、action、reducer、index 等
 - 然后使用combineReducers对多个模块合并，这种代码组织方式过于繁琐和麻烦，导致代码量过多，也不利于后期管理
 - Redux Toolkit 就是**为了解决这种编码方式而诞生**。
 - **并且以前的 createStore 方式已标为过时，而 Redux Toolit 已成为官方推荐**；

Redux Toolkit的核心API主要是如下几个：
 - **configureStore**：包装createStore以提供简化的配置选项和良好的默认值。
	 - **可自动组合 slice reducer**
	 - 可添加其它 Redux 中间件，redux-thunk默认包含，
	 - 默认启用 Redux DevTools Extension
 - **createSlice**：接受切片名称、初始状态值和reducer函数的对象，并自动生成切片reducer，并带有相应的actions。
 - **createAsyncThunk**: 接受一个动作类型字符串和一个返回承诺的函数，并生成一个pending/fulfilled/rejected基于该承诺分派动作类型的thunk。简单理解就是**专门用来创建异步Action。**

## 5.1 创建counter模块的reducer

createSlice主要包含如下几个参数：
 - name：用来标记slice的名词
	 - redux-devtool中会显示对应的名词；
 - initialState：第一次初始化时的值；
 - reducers：相当于之前的reducer函
	 - 对象类型，并且可以添加很多的函数
	 - 函数类似于redux原来reducer中的一个case语句
	 - 函数的参数：
		 - 参数一：state
		 - 参数二：action
 - createSlice 返回值是一个对象
	 - 对象包含所有的 actions 和 reducer；

```js
// src/soters/counter.js
import { createSlice } from "@reduxjs/toolkit"
const counterStore = createSlice({
  name: "home",
  initialState: {
    counter: 0,
  },
  reducers: {
    increment(state) {
      state.counter += 1
    },
  }
})

export const { increment } = counterStore.actions
export default counterStore.reducer
```

## 5.2 store的创建

configureStore用于创建store对象，常见参数如下：

 - reducer，将slice中的reducer可以组成一个对象传入此处；
 - middleware：可以使用参数，传入其他的中间件（自行了解）；
 - devTools：是否配置devTools工具，默认为true；

```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from './counter'
const store = configureStore({
  reducer: {
    home: counterReducer,
  }
})

export default store
```

## 5.3 store接入应用

在app.js中将store接入应用：

 - Provider，内容提供者，给所有的子或孙子组件提供store对象；
 - store： 使用configureStore创建的store对象；


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774439006000ez13if.png)

## 5.4 开始使用store

函数式组件中可以使用 react-redux 提供的 Hooks API 连接、操作 store。

 - useSelector 允许你使用 selector 函数从 store 中获取数据（root state）。
 - useDispatch 返回 redux store 的 dispatch 引用。你可以使用它来 dispatch actions。
 - useStore 返回一个 store 引用，和 Provider 组件引用完全一致。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774439156000jwgptd.png)


## 5.5 Redux Toolkit异步Action操作

在之前的开发中，我们通过redux-thunk中间件让dispatch中可以进行异步操作。

Redux Toolkit默认已经给我们继承了Thunk相关的功能：createAsyncThunk

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774439193000pl375c.png)


当createAsyncThunk创建出来的action被dispatch时，会存在三种状态：

 - pending：action被发出，但是还没有最终的结果；
 - fulfilled：获取到最终的结果（有返回值的结果）；
 - rejected：执行过程中有错误或者抛出了异常；

我们可以在createSlice的entraReducer中监听这些结果

 - **extraReducers也支持函数，该函数会接收一个builder参数**
 - builder.addCase(getHomeMultidataAction.fulfilled, (state, action)=>{} )

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774439257000tji89c.png)

