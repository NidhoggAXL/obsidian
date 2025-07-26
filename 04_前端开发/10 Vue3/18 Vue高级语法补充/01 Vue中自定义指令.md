
# 一、认识自定义指令

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/175317359900028pw4l.png)

## 1.1 实现方式一：聚焦的默认实现

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753173643000rcj95d.png)

## 1.2 实现方式二：局部自定义指令
实现方式二：自定义一个 v-focus 的局部指令 

* 这个自定义指令实现非常简单，我们只需要在组件选项中使用 **directives** 即可； 
* 它是一个对象，在对象中编写我们自定义指令的名称（注意：<mark class="hltr-orange">这里不需要加v-</mark>）； 
* 自定义指令有一个生命周期，是在组件挂载后调用的 **mounted**，我们可以在其中完成操作；

```html
<script>
// 自定义指令:option API使用
export default {
  directives: {
    focus: {
      mounted(el) {
        // console.log(el)
        // <input type="text />
        //el 是指令绑定的元素
        el.focus()
      }
    }
  }
 }
</script>

<script setup>
//使用setup来定义自定义指令
const vFocus = {
  mounted(el) {
    // console.log(el)
    // <input type="text />
    //el 是指令绑定的元素
    el.focus()
  }
}
</script>

<template>
  <div class="app">
    <input type="text" v-focus />
  </div>
</template> 

<style lang="less" scoped>

</style>
```

## 1.3 方式三：自定义全局指令

在main.js中自定义一个全局的v-focus指令可以让我们在任何地方直接使用

```js
import { createApp } from 'vue'
import App from './01 自定义指令/App.vue'

const app = createApp(App)

app.directive('focus', {
  mounted(el) {
    // el 是指令绑定的元素
    el.focus()
  }
})

app.mount('#app')
```

### 全局定义封装

创建 directives 问价夹 -> 创建全局指令编码 -> 创建 index.js 文件统一运行（防止main中多次调用）-> main文件引入（只调用一次就好）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753180716000t8hrqy.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753180741000cdf4fk.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753180752000jjn2wv.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17531807760008ibttc.png)

# 二、指令的生命周期
一个指令定义的对象，Vue提供了如下的几个钩子函数： 

* **created**：在绑定元素的 attribute 或事件监听器被应用之前调用；
* **beforeMount**：当指令第一次绑定到元素并且在挂载父组件之前调用； 
* **mounted**：在绑定元素的父组件被挂载后调用； 
* **beforeUpdate**：在更新包含组件的 VNode 之前调用； 
* **updated**：在包含组件的 VNode 及其子组件的 VNode 更新后调用； 
* **beforeUnmount**：在卸载绑定元素的父组件之前调用； 
* **unmounted**：当指令与元素解除绑定且父组件已卸载时，只调用一次；

> [!tip] VNode 就是内容数据

# 三、指令的参数和修饰符

如果我们指令需要接受一些参数或者修饰符应该如何操作呢？ 

* info是参数的名称； 
* aaa-bbb是修饰符的名称； 
* 后面是传入的具体的值；

在我们的生命周期中，我们可以通过 **bindings** 获取到对应的内容：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534026230004ma1ge.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534026310000oz20g.png)

> [!info] modifiers - 修饰符
## 3.1 自定义指令练习

自定义指令案例：时间戳的显示需求： 

* 在开发中，大多数情况下从服务器获取到的都是时间戳； 
* 我们需要将时间戳转换成具体格式化的时间来展示； 
* 在Vue2中我们可以通过[[03 JQuery的整体架构#四、jQuery过滤器（filtering）的API|过滤器]]来完成； 
* 在Vue3中我们可以通过 计算属性（computed） 或者 自定义一个方法（methods） 来完成； 
* 其实我们还可以通过一个自定义的指令来完成；

我们来实现一个可以自动对时间格式化的指令v-format-time： 

* 这里我封装了一个函数，在首页中我们只需要调用这个函数并且传入app即可；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753403793000i0p37o.png)

> [!tip] content如果没有进行隐式转换的话，最好还是添加一个`Number(timestamp)`

