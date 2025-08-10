# 一、setup函数的参数

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746885610000v5j7sj.png)

# 二、setup函数的返回值
setup既然是一个函数，那么它也可以有返回值，它的返回值用来做什么呢？ 

* setup的返回值可以在<mark class="hltr-orange">模板template中被使用</mark>； 
* 也就是说我们可以<mark class="hltr-orange">通过setup的返回值来替代data选项</mark>；

甚至是我们可以<mark class="hltr-orange">返回一个执行函数</mark>来<mark class="hltr-orange">代替在methods中定义的方法</mark>：

```html
<template>
  <div class="app">
    <h2>{{ message }}</h2>
    <h3>Count: {{ count }}</h3>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
  </div>
</template>

<script>
export default {
  setup() {
    const message = 'Hello, Vue3 !';
    let count = 0;
    const increment = () => {
      count++;
      //看看 count 的值是否改变
      console.log(count)
    };
    const decrement = () => {
      count--;
    };
    //返回值（对象）会被暴露到模板中
    return {
      message,
      count,
      increment,
      decrement,
    };
  }
}
</script>

<style scoped>

</style>
```

但是，如果我们将 counter 在 increment 或者 decrement进行操作时，**是否可以实现界面的响应式呢？** 

* 答案是<mark class="hltr-orange">不可以</mark>； 
* 这是因为对于一个<mark class="hltr-orange">定义的变量</mark>来说，默认情况下，<mark class="hltr-orange">Vue并不会跟踪它的变化，来引起界面的响应式操作；</mark>

当点击increment按钮后，回发现通过<mark class="hltr-orange">插值语法插入的 count 并没有改变</mark>，但是在 setup 中定义的发送了改变：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746886344000tbk2ms.png)



