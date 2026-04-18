# 一、全局状态共享

Nuxt跨页面、跨组件全局状态共享可使用 useState（支持Server和Client ）：

 - `useState<T>(init?: () => T | Ref<T>): Ref<T>`
 - `useState<T>(key: string, init?: () => T | Ref<T>): Ref<T>`
 - 参数:
	 - init：为状态**提供初始值的函数**，该函数也支持返回一个Ref类型
	 - key: 唯一key，确保在跨请求获取该数据时，保证数据的唯一性。**为空时会根据文件和行号自动生成唯一key**
 - 返回值：Ref 响应式对象

useState 具体使用步骤如下：

1. 在 composables 目录下创建一个模块，如： composables/counter.ts
2. 在useCounter.ts中使用 useState 定义需全局共享状态，并导出

```ts
// useCounter.ts
export default function () {
  return useState("counter", () => 100)
}
```

2. 在组件中使用 useCounter.ts 导出的全局状态

```vue
<script setup>
const counter = useCounter()
function addCounter() {
  counter.value ++
}
</script>

<template>
  <div class="app">
    <h1>首页</h1>
    <h1> {{ counter }}</h1>
    <button @click="addCounter">+1</button>
  </div>
</template>

<style scoped>

</style>
```

> [!tip]
> useState 注意事项:
> - useState 只能用在 setup 函数 和 Lifecycle Hooks 中
> - useState 不支持classes, functions or symbols类型，因为这些类型不支持序列化

# 二、Nuxt基础Pinia

安装依赖

 - npm install @pinia/nuxt –-save
	 - @pinia/nuxt 会处理state同步问题，比如不需要关心序列化或XSS 攻击等问题
 - npm install pinia –-save
	 - 如有遇到pinia安装失败，可以添加 --legacy-peer-deps 告诉 NPM 忽略对等依赖并继续安装。或使用yarn

Nuxt 应用接入 Pinia

- 如果是创建在 app/stores 创建的 store 不需要导入，Nuxt回自动导入，也可以通过配置，确定那里的 store 自动导入:https://nuxt.com.cn/modules/pinia
- 在nuxt.config文件中添加： `modules: [‘@pinia/nuxt‘] `，如下图所示：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17742401300001v0iel.png)

# 三、Pinia 使用步骤

Pinia 使用步骤：

 - 1.在app/stores文件夹中定义一个模块，比如：stores/counter.ts
 - 2.在 stores/counter.ts 中使用 defineStore函数 来定义 store 对象
 - 3.在组件中使用定义好的 store 对象

```ts
// app/stores/counter.ts
import { defineStore } from 'pinia'
export const useCounterStore = defineStore("counter", {
  state() {
    return {
      counter: 0
    }
  },
  actions: {
    increment() {
      this.counter++
    },
    decrement() {
      this.counter--
    }
  }
})
```

使用：

```vue
<script setup>
const homeStore = useCounterStore()
const { counter } = storeToRefs(homeStore)
function handleCounter() {
  homeStore.increment()
}
</script>

<template>
  <div class="home">
    <h1>{{ counter }}</h1>
    <button @click="handleCounter">+1</button>
  </div>
</template>

<style lang="less" scoped>

</style>
```


