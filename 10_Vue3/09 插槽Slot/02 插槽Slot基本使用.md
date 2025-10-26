# 一、插槽的基本使用

**要求是: App.vue 文件里面确定插槽的内容(例如按钮、图片)：**

子组件的代码如下：

```html
<template>
 <div class="show-message">
   <h1>{{ message }}</h1>
   <slot></slot>
   <p>这是一个插槽的例子</p>
 </div>
</template>

<script>
export default {
 props: {
  message: {
   type: String,
   default: 'message的默认值'
  }
 }
}
</script>

<style scoped>

</style>
```

父组件代码如下：


```html
<template>
 <div class="app">
  <!-- 父元素使用按钮来占位插槽 -->
  <show-message message="按钮插槽">
   <button>我是按钮的插槽</button>
  </show-message>

  <!-- 父元素使用图片来占位插槽 -->
   <show-message message="图片插槽">
    <img src="https://www.imooc.com/static/img/index/logo.png" alt="logo" />
   </show-message>
 </div>
</template>

<script>
import ShowMessage from './ShowMessage.vue';
export default {
 components: {
   ShowMessage 
 }
}
</script>

<style scoped>

</style>
```

页面效果：

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746780203000gjgn03.png)


# 二、插槽的默认内容

有时候我们希望在使用插槽时，如果**没有插入对应的内容**，那么我们需要显示一个<mark class="hltr-orange">默认的内容： </mark>

当然这个默认的内容只会在没有提供插入的内容时，才会显示；


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746780383000o5g3v5.png)

