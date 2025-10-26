# 一、setup函数的参数

我们先来研究一个setup函数的参数，它主要有两个参数:

- 第一个参数:props
- 第二个参数:context

props非常好理解，它其实就是**父组件传递**过来的**属性**会被**放到props对象中**，我们在setup中如果需要使用，那么就可以直接通过props参数获取:

-  对于定义props的类型，还是和之前的options API规则是一样的，在**props选项中定义**
- 并且在template中依然是可以正常去使用props中的属性，比如message;
- **如果在setup函数中想要使用props，那么不可以通过 this 去获取**
- 因为props有直接作为参数传递到setup函数中，所以我们可以**直接通过参数来使用即可**

另外一个参数是context，我们也称之为是一个SetupContext，它里面包含三个属性:

- **attrs**：所有的非prop的attribute;
- **slots**：父组件传递过来的插槽
- **emit**：当我们组件内部需要发出事件时会用到emit(因为我们不能访问this，所以不可以通过 this.$emit发出事件);

# 二、setup函数的返回值

setup既然是一个函数，那么它也可以有返回值，它的返回值用来做什么呢？ 

* setup的返回值可以在模板template中被使用； 
* 也就是说可以通过**setup的返回值来替代data选项**；

甚至是我们可以返回一个执行函数来代替在methods中定义的方法：

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

* 答案是不可以； 
* 这是因为对于一个定义的变量来说，默认情况下，Vue并不会跟踪它的变化，来引起界面的响应式操作；

当点击increment按钮后，回发现通过插值语法插入的 count 并没有改变，但是在 setup 中定义的发送了改变：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746886344000tbk2ms.png)



