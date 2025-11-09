# 一、认识和定义State

state 是 store 的核心部分，因为store是用来帮助我们管理状态的。 

* 在 Pinia 中，状态被定义为返回初始状态的函数；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159506000ip73is.png)


# 二、操作State

## 2.1 读取和写入

**读取和写入 state**：  默认情况下，您可以通过 store 实例访问状态来直接读取和写入状态；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159556000bsk5ko.png)

## 2.2 $reset重置

**重置 State**： 你可以通过调用 store 上的 <mark class="hltr-cyan">$reset() 方法将状态重置到其初始值</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159571000yyccs2.png)

## 2.3 $patch多修改

**改变State：** 

* 除了直接用 store.counter++ 修改 store，你还可以调用 $patch 方法； 
* 它允许您使用部分“state”对象<mark class="hltr-cyan">同时应用多个更改</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159608000n60o9i.png)

## 2.4 $state替换

**替换State**：

* 可以通过将其 $state 属性设置为新对象来替换 Store 的整个状态：
* 但是这里的替换更像是一种合并，替换后的对象和原对象地址相同
* 也可以进行重置State

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159700000dhcti8.png)

# 三、State原始数据

state的本质其实是一个代理对象(Proxy)，这样他才可以做到响应式，那如何拿到原始的对象呢，而不是一个代理对象呢？

## 3.1 storeToRefs(推荐)

```js
import { storeToRefs } from 'pinia'
import { useCounterStore } from '@/stores/counter'

const counterStore = useCounterStore()
const { count, name } = storeToRefs(counterStore)
```

这样解构出来的值会保持响应性，但不是Proxy对象

## 3.2 JSON.parse(JSON.stringify())

```js
const counterStore = useCounterStore()
const originalState = JSON.parse(JSON.stringify(counterStore.$state))
```

这种方法会创建一个完全独立的对象副本，不包含任何响应性或Proxy特性。

## 3.3 toRaw

```js
import { toRaw } from 'vue'
import { useCounterStore } from '@/stores/counter'

const counterStore = useCounterStore()
const originalState = toRaw(counterStore.$state)
```

`toRaw`会返回由`reactive`或`readonly`转换的原始对象。

## 3.4 $state

```js
const counterStore = useCounterStore()
const state = counterStore.$state
```

虽然这仍然是响应式的，但它是store的原始状态对象。

## 总结

需要注意的是，如果你需要保持数据的响应性，推荐使用第一种方法`storeToRefs`。如果你只需要一个静态的快照数据，可以使用第二种或第三种方法。


