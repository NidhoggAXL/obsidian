# 一、认识生命周期

什么是生命周期呢?

- 生物学上，生物生命周期指得是一个生物体在生命开始到结束周而复始所历经的一系列变化过程;
- 每个组件都可能会经历从**创建、挂载、更新、卸载**等一系列的过程
- 在这个过程中的**某一个阶段**，可能会想要**添加一些属于自己的代码逻辑**(比如组件创建完后就请求一些服务器数据)
- 但是如何可以知道目前组件正在哪一个过程呢?Vue给我们提供了组件的生命周期函数

生命周期函数:

- 生命周期函数是一些钩子函数(**回调函数**)，在某个时间会被Vue源码内部进行回调,
- 通过对生命周期函数的回调，我们可以知道目前组件正在经历什么阶段，
- 那么我们就可以在该生命周期中编写属于自己的逻辑代码了:
# 二、生命周期的流程

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746800835000pi45h6.png)


Vue的生命周期函数

* beforeCreate :组件实例在创建之前
* created: 组件被创建完成
	* 可以发送网络请求
	- 可以事件监听
	- this.$watch()
- beforeMount : 组件template准备被挂载
- mounted :组件template已经被挂载
	- 可以获取DOM,可以使用DOM
- beforeUpdate: 准备更新DOM
- updated: 更新DOM,根据最新数据生成新的VNode,生成新的虚拟DOM,转换为真实的DOM
- beforeUnmount: 卸载之前
- unmounted: DOM 元素被卸载完成
	- 回收操作(取消事件监听)


```js
export default {
  // 1.组件被创建之前
  beforeCreate() {
    console.log("beforeCreate")
  },
  // 2.组件被创建完成
  created() {
    console.log("created")
    console.log("1.发送网络请求, 请求数据")
    console.log("2.监听eventbus事件")
    console.log("3.监听watch数据")
  },
  // 3.组件template准备被挂载
  beforeMount() {
    console.log("beforeMount")
  },
  // 4.组件template被挂载: 虚拟DOM -> 真实DOM
  mounted() {
    console.log("mounted")
    console.log("1.获取DOM")
    console.log("2.使用DOM")
  },
  // 5.数据发生改变
  // 5.1. 准备更新DOM
  beforeUpdate() {
    console.log("beforeUpdate")
  },
  // 5.2. 更新DOM
  updated() {
    console.log("updated")
  },

  // 6.卸载VNode -> DOM元素
  // 6.1.卸载之前
  beforeUnmount() {
    console.log("beforeUnmount")
  },
  // 6.2.DOM元素被卸载完成
  unmounted() {
    console.log("unmounted")
  }
}
```

