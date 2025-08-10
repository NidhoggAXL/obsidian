# 一、$refs的作用
某些情况下，我们在组件中想要**直接获取到元素对象或者子组件实例**： 

* 在Vue开发中我们是<mark class="hltr-orange">不推荐进行原生DOM操作</mark>的； 
* 这个时候，我们可以<mark class="hltr-orange">给元素或者组件绑定一个ref的attribute属性</mark>；

组件实例有一个$refs属性： 

* 它一个对象Object，持有注册过 ref attribute 的所有 DOM 元素和组件实例。

在App.vue 和 banner.vue 子组件里面都存在 ref 属性的元素
```html
<template>
 <div class="app">
  <h2 ref="title">07 ref使用</h2>
  <button @click="btn">按钮</button>
 </div>
</template>

<script>
export default {
 methods: {
  btn() {
   //访问元素
   console.log(this.$refs.title);
   //访问组件实例
   console.log(this.$refs.title.$el);
   //在父组件中可以主动的调用子组件的对象方法
   this.$refs.banner.show();
   //获取banner组件实例，获取banner中的元素
   this.$refs.banner.$el;
  }
 }
}
</script>

<style scoped>

</style>
```

# 二、`$`parent和`$`root

可以通过$parent来访问父元素。 

可以通过$root来访问根元素。 

```js
console.log(this.$parent)
console.log(this.$root)
```



