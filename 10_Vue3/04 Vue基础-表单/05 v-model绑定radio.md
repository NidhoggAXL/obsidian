在 input 的 type 为 [[01 高级元素的使用#5.5 input作为单选框 radio|radio(单选框)]] 的时候，如果 **v-model 绑定的是同一个值，本身就是会互斥的。**

使用 v-model 来进行互斥：(默认选择女)

* 必须要有 value 才知道 v-model 绑定的值里面是什么数据

```html
<body>
 <div id="app">
 
  <label for="male">
   <input id="male" type="radio" v-model="gender" value="male"> 男
  </label>
  
  <label for="female">
   <input id="female" type="radio" v-model="gender" value="female"> 女
  </label>
  
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data() {
    return {
     //把input里面的value通过v-model绑定到gender上面
     gender: 'female' // 默认选中女
    }
   }
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```


