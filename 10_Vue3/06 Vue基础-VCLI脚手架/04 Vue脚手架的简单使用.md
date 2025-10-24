# 一、使用全局脚手架

## 1.1 根组件挂载

首先定义一个 product.vue 组件：会使用到 ES Module 里面的ES module中export的[[05 ES Module用法详解#六、default用法|defalut]]来进行**导出**

```html
<template>
 <h2>我是一个vue模块化的{{ message }}</h2>
</template>

<script>
//默认导出
export default {
 data() {
  return {
   message: '我是product'
  }
 }
}
</script>

<style>
 h2 {
  color: red;
 }
</style>
```

然后再在 main.js 里面进行一个导入，并创建APP挂在到 app 上面

```js
import { createApp } from 'vue'

//导入product组件
import Product from './product.vue'

//创建App的根组件，并挂在到#app上面（id为app）
createApp(Product).mount('#app')
```


index.html 里面的文件格式：

```html
<body>
    <div id="app"></div>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746178725000eqisbg.png)

## 1.2 其他组件挂载到根组件

首先也是创建 demo.vue 组建：

```html
<template>
 <h2>{{ title }}</h2>
 <p>我是demo的一个段落</p>
</template>

<script>
export default {
 data() {
  return {
    title: "我是标题"
   }
  }
 }
</script>

<style>
 h2 {
  color: red;
 }
</style>
```

然后在 main.js 里面导入并注册组件：

```js
import { createApp } from 'vue'

//导入product组件
import Product from './product.vue'
// 导入demo组件
import Demo from './demo.vue'

//创建app根组件
const app = createApp(Product)

// 注册全局demo组件
app.component("demo-component", Demo)

//把app根组件挂在到#app上面
app.mount('#app')
```

居然挂在到了根组件上面，那么就可以在根组件 product 的 template 中使用：

```html
<template>
 <h2>我是一个vue模块化的{{ message }}</h2>
 <demo-component></demo-component>
</template>
```

> [!tip] 特别注意
> 不是直接到 index.html 中去使用组件，如果要到 html 中使用的话，那么根组件的 template 也要在 html 中。


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746178736000mj7czu.png)

# 二、使用局部组件

以上面的 [[#1.2 其他组件挂在到根组件|其他组件挂载到根组件]] 为例，让 demo 为局部组件的话，需要到 product.vue 里面设置 [[06 Vue的options|options]] 的 components。

首先需要把 main.js 里面的全局注册删除：

```js
import { createApp } from 'vue'

//导入product组件
import Product from './product.vue'
// 导入demo组件
import Demo from './demo.vue'

//创建app根组件
const app = createApp(Product)

// 注册全局demo组件
// app.component("demo-component", Demo)

//把app根组件挂在到#app上面
app.mount('#app')

```

使用局部组件就需要在 product.vue 里面导入 demo.vue 的组件：[[03 注册Vue的布局组件|布局组件]]

```html
<template>
 <h2>{{ message }}</h2>
 <demo-component></demo-component>
</template>

<script>
// 导入demo组件,组件名使用的是驼峰标识法
//使用的时候就可以 demo-component
import DemoComponent from './demo'

export default {
 data() {
  return {
   message: '我是product'
  }
 },
 // 注册局部组件
 components: {
  // 对象增强写法
  DemoComponent
 }
}
</script>

<style>
 h2 {
  color: red;
 }
</style>
```




