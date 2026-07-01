# 一、v-model的基本使用

表单提交是开发中非常常见的功能，也是和用户交互的重要手段： 

* 比如用户在**登录、注册**时需要提交账号密码；
* 比如用户在**检索、创建、更新**信息时，需要提交一些数据；

这些都要求我们可以在代码逻辑中获取到用户提交的数据，我们通常会使用v-model指令来完成： 

* **v-model指令**可以在表单 [](05_前端基础/01%20HTML%20+%20CSS/05%20高级元素/01%20高级元素的使用.md#5.1%20input|input)、[](05_前端基础/01%20HTML%20+%20CSS/05%20高级元素/01%20高级元素的使用.md#5.7%20textarea%20的使用|textarea) 以及 [](05_前端基础/01%20HTML%20+%20CSS/05%20高级元素/01%20高级元素的使用.md#5.8%20select%20和%20option%20的使用|select) 元素上创建**双向数据绑定**； 
* 它会根据**控件类型**自动选取正确的方法来更新元素； 
* 尽管有些神奇，**但 v-model 本质上不过是语法糖**，它**负责监听用户的输入事件来更新数据**，并在某种极端场景下进行一些特殊处理；

使用到的技术：[](01%20高级元素的使用#五、表单元素#五、表单元素#5.4%20input%20和%20label%20的关系|label) 和 [placeholder](05_前端基础/01%20HTML%20+%20CSS/08%20HTML5/03%20input元素的扩展内容.md)

```html
<body>
 <div id="app">
  <label for="username">
   <input id="username" type="text" v-model="name" placeholder="请输入姓名" />
   <span>{{ name }}</span>
  </label>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data() {
    return {
     name: ''
    }
   }
  })
  
  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

>[!ps]
>当在输入框中输入的时候，data 中的 name 也是会发生改变的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17459321450004w4q5a.png)


