# 一、简单使用
在 vue 开发中是一个组件的开发，并不希望组件之间相互影响，但是 style 本身是一个选择器，并没有作用域的。

例如：在 App.vue 根组件下面这是的style会影响到引入的其他局部组件。

**创建的 demo 组价：**

```html
<template>
  <h2 class="title">我是demo中的h2标题</h2>
  <p>这是一个demo的描述!</p>
</template>

<script>
export default {

 }
</script>

<style></style>
```

在 App.vue 里面引入 demo.vue 组件并设置 .title 的样式:

```html
<template>
 <h2 class="title">我是app中的标题h2</h2>
 <demo-header></demo-header>
</template>

<script>
//导入demo组件
import DemoHeader from './demo.vue'

export default {
 name: 'App',
 //创建App的局部组件
 components: {
   DemoHeader
  }
 }
</script>

<style >
 .title {
  color: red;
 }
</style>
```

会发现在 App.vue 里面设置的style会影响到 demo.vue 的组件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746259679000tek3zk.png)

要解决这个问题,那么就需要为style设置scoped（作用域）的属性

* 本质是为元素自动添加不同的 <mark class="hltr-orange">data- 属性</mark>

```html
<style scoped> </style>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747143794000r7x1fr.png)

>[!tip] 在开发中
>基本上所有的style都希望设计自己的组件,不要和其他的有影响所以基本<mark class="hltr-orange">都需要为style添加 scoped(作用域) 属性</mark>

# 二、BUG
如果子组件并没有<mark class="hltr-orange">进行一个包裹</mark>的时候，这个 style 的 scoped 就不生效：

demo.vue 子组件：

```html
<template>
 <div class="demo">
  <h2 class="title">demo里面的title</h2>
 </div>
</template>

<script>
export default {

}
</script>

<style scoped>

</style>
```

App.vue 根组件：

```html
<template>
 <div class="app">
  <h2 class="title">我是App里面的</h2>
  <Demo></Demo>
 </div>
</template>

<script>
import Demo from './demo.vue'
export default {
 components: {
  Demo
 },
}
</script>

<style scoped>
 .title {
  color: red;
 }
</style>
```

<mark class="hltr-orange">这个时候的 data-属性 会变成相同的</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747143854000aa08hd.png)

