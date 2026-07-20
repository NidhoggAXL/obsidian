# 一、script setup语法

`<script setup>` 是在[[01 Vue的开发模式解析|单文件组件 (SFC)]] 中使用组合式 Composition API 的编译时语法糖，当同时使用 SFC 与组合式 API 时则推荐该语法。

* 更少的样板内容，更简洁的代码；
* 能够使用纯 Typescript 声明 prop 和抛出事件；
* 更好的运行时性能 ；
* 更好的 IDE 类型推断性能 ；

使用这个语法，需要将 setup attribute 添加到`<script>`代码块上

```vue
<template>
 <h2>{{ message }}</h2>
</template>

<script setup>
 const message = 'Hello World'
</script>

<style scoped>

</style>
```

**里面的代码会被编译成组件 setup() 函数的内容：** 

* 这意味着与普通的`<script>`只在组件被首次引入的时候执行一次不同；
* `<script setup>`中的代码会在每次组件实例被创建的时候执行。

# 二、顶层的绑定会被暴露给模板

当使用`<script setup>`的时候，任何在`<script setup>`声明的**顶层绑定**(包括变量，函数声明，以及 import 引入的内容) 都能在**模板中直接使用**：

> [!abstract]
> 
> 简单理解就是在 setup 作用域里面的，如果是如下面的name就是在foo作用域里面的，而bushfire在setup作用域里面，就不符合顶层的绑定。

```vue
<template>
 <h2>{{ message }}</h2>
</template>

<script setup>
//message暴露到顶层作用域
const message = 'Hello World'
function foo() {
	//name没有暴露到顶层作用域
	const name = "axl"
}
</script>

<style scoped>

</style>
```

> [!tip] 注意点：
> 响应式数据需要通过ref、reactive来创建。

# 三、导入的组件直接使用

`<script setup>`范围里的值也能被直接作为自定义组件的标签名使用：

```vue
<template>
 <useCounter></useCounter>
</template>

<script setup>
import useCounter from './useCounter';
</script>

<style scoped>

</style>
```

# 四、defineProps 和 defineEmits

为了在声明 props 和 emits 选项时获得**完整的类型推断支持**，我们可以使用 defineProps 和 defineEmits API，它们将自动地在`<script setup>`中可用

```vue
<template>
  <h2>ShowInfo: {{ name }} - {{ age }}</h2>
  <button @click="changeAge">修改age</button>
</template>

<script setup>
const props = defineProps({
  name: {
    type: String,
    default: ""
  },
  age: {
    type: Number,
    default: 0
  }
});

const emit = defineEmits(["changeAge"]);

function changeAge() {
  emit("changeAge", 200);
}
</script>
```

# 五、defineExpose

在Opsition API中通过 [[02 组件中的ref引用|$ref]] 取到组件的公开实例，而在composition API中不会主动的暴露任何在 `<script setup>` 中声明的绑定

通过 defineExpose 编译器宏来显示指定在 `<script setup>` 组件中要暴露出去的 property；

子组件的编写：

```js
function foo() {
  console.log("foo function")
}

defineExpost({
 //对象的增强写法
 foo
})
```

父组件的编写：

* 父组件里面来使用子组件实例的foo方法

```js
const showInfoRef = ref(null)
function callShowInfo() {
  showInfoRef.value.foo()
}
```

