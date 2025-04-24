# 一、v-once指令（了解）

v-once用于指定元素或者组件只渲染一次： 

* 当数据发生变化时，元素或者组件以及其所有的子元素将视为静态内容并且跳过； 
* 该指令可以用于性能优化；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17454949400007m06eg.png)

如果是子节点，也是只会渲染一次：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745494963000u72emo.png)


```html
<body>
 <div id="app">
  <h2 v-once>{{message}}</h2>
  <!-- 点击按钮只会改变message一次 -->
  <button @click="changeMessage">改变message</button>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data: function() {
    return {
     message: 'hello Vue'
    }
   },
   methods: {
    // 定义一个方法
    changeMessage: function() {
     this.message = '改变了message'
     console.log(this.message)
     //点击按钮打印 改变了message
    }
   }
  })
  
  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

> 当点击 button 的时候，message并不会改变，但是数据本身时发生了改变的。



