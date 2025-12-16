# 一、编译配置(config)

编译配置存放于项目根目录下的 config 目录中，包含三个文件：

 - index.js 是**通用**配置
 - dev.js 是项目**开发时**的配置
 - prod.js 是项目**生产时**的配置

常用的配置

 - projectName ： 项目名称
 - date ： 项目创建时间
 - designWidth: 设计稿尺寸
 - sourceRoot : 项目源码目录
 - **outputRoot： 项目产出目录**
 - **defineConstants: 定义全局的变量（DefinePlugin）**
 - **alias: 配置路径别名**
 - h5.webpackChain： webpack配置
 - h5.devServer ：开发者服务配置
 - 更多的配置：https://docs.taro.zone/docs/config

```js title = "alias配置"
alias: {
  "@": path.resolve(__dirname, "..", "src"),//别名
}
```

# 二、全局配置(app.config.js)

app.config.js 用来对小程序进行全局配置，配置项遵循微信小程序规范，类似微信小程序的app.json，并对所有平台进行统一

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765866793000016hs9.png)

```js
// app.config.js
export default defineAppConfig({
  pages: ["pages/index/index"],
  window: {
    backgroundTextStyle: "light",
    navigationBarBackgroundColor: "#fff",
    navigationBarTitleText: "WeChat",
    navigationBarTextStyle: "black",
  },
});
```

> [!tip] 更多的配置：https://docs.taro.zone/docs/next/app-config

# 三、页面配置(.config.js)

一个小程序页面都可以使用 .config.js 文件来**对本页面的窗口表现进行配置**。

页面中配置项在当前页面会**覆盖全局配置** app.config.json 的 window 中相同的配置项。

文件需要 export 一个默认对象，配置项**遵循微信小程序规范**，并且对所有平台进行统一。

更多页面配置：https://docs.taro.zone/docs/next/page-config

```js
// page.config.js
// 对每个页面的小程序配置
export default definePageConfig({
  navigationBarTitleText: "首页",
});

```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765868866000dvcpa5.png)


# 四、项目配置(project.x.json)


了适配不同的小程序， Taro支持各个小程序平台添加各自项目配置文件。

 - 默认 project.config.json 配置只能用于微信小程序。

project.config.json 常用配置

 - libVersion 小程序基础库版本
 - projectname 小程序项目名字
 - appid 小程序项目的appid
 - setting 小程序项目编译配置

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765868912000wwow5y.png)


# 五、入口组件(app.js)

https://docs.taro.zone/docs/react-entry

每一个 Taro 应用都需要一个入口组件（如React 组件）用来注册应用。入口文件默认是 src 目录下的 app.js。

在入口app.js组件中我们可以: 

 - 定义应用的生命周期
	 - onLaunch -> useEffect：在小程序环境中对应 app 的 onLaunch。
	 - componentDidShow -> useDidShow：在小程序环境中对应 app 的 onShow 。
	 - componentDidHide -> useDidHide：在小程序环境中对应 app 的 onHide 。
 - 定义应用的全局状态：Redux ( Vuex、Pinia)



```js title="类组件"
import React, { Component } from 'react'

// 假设我们要使用 Redux
import { Provider } from 'react-redux'
import configStore from './store'

// 全局样式
import './app.css'

const store = configStore()

class App extends Component {
  // 可以使用所有的 React 生命周期方法
  componentDidMount() {}

  // 对应 onLaunch
  onLaunch() {}

  // 对应 onShow
  componentDidShow() {}

  // 对应 onHide
  componentDidHide() {}

  render() {
    // 在入口组件不会渲染任何内容，但我们可以在这里做类似于状态管理的事情
    return (
      <Provider store={store}>
        {/* this.props.children 是将要被渲染的页面 */}
        {this.props.children}
      </Provider>
    )
  }
}

export default App
```

```js title = "函数组件"
import React, { useEffect } from 'react'

// Taro 额外添加的 hooks 要从 '@tarojs/taro' 中引入
import { useDidShow, useDidHide } from '@tarojs/taro'

// 假设我们要使用 Redux
import { Provider } from 'react-redux'
import configStore from './store'

// 全局样式
import './app.css'

const store = configStore()

function App(props) {
  // 可以使用所有的 React Hooks
  useEffect(() => {})

  // 对应 onShow
  useDidShow(() => {})

  // 对应 onHide
  useDidHide(() => {})

  return (
    // 在入口组件不会渲染任何内容，但我们可以在这里做类似于状态管理的事情
    <Provider store={store}>
      {/* props.children 是将要被渲染的页面 */}
      {props.children}
    </Provider>
  )
}

export default App
```


