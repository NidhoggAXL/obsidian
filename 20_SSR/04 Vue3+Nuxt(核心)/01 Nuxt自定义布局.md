Layout布局是**页面的包装器**，可以将多个页面**共性东西抽取到 Layout布局** 中。

 - 例如：每个页面的页眉和页脚组件，这些具有共性的组件我们是可以写到一个Layout布局中。

Layout布局是使用 **`<slot>`** 组件来显示页面中的内容

Layout布局有两种使用方式：

 方式一：默认布
 
 - 在layouts目录下新建默认的布局组件，比如：layouts/default.vue
 - 然后在app.vue中通过`<NuxtLayout>`内置组件来使用

```vue
// app/layout/default.vue
<script setup>

</script>

<template>
  <div class="loayout-default">
    <h1 class="header">header</h1>
    <!-- 插槽,被这个layout包裹的内容就插入到这里 -->
    <slot></slot>
    <h1 class="footer">footer</h1>
  </div>
</template>

<style lang="less" scoped>
.header {
  font-size: 20px;
  color: red;
  background-color: #ccc;
}
.footer {
  font-size: 20px;
  color: blue;
  background-color: #ccc;
}
</style>
```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774017481000dlyo4s.png)


 方式二：自定义布局（Custom Layout）
 
 - 继续在layouts文件夹下新建 Layout 布局组件，比如: layouts/custom-layout.vue
 - 然后在app.vue中给`<NuxtLayout>`内置组件 指定name属性 的值为：custom-layout
	 - 也支持在页面中使用 definePageMeta 宏函数来指定 layout 布局
	 - **使用 definePageMeta 定义 layout 布局的时候，需要在 app.vue 里面使用 `<NuxtLayout>` 先进行包裹。**




