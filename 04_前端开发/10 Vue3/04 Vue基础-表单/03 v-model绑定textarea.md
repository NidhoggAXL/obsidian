
什么是：[[01 高级元素的使用#5.7 textarea 的使用|textarea]]

```html
<body>
 <div id="app">
  <textarea v-model="current" cols="30" rows="10"></textarea>
  <p>article当前的值是:{{ current }}</p>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data() {
    return {
     current: ''
    }
   }
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```
