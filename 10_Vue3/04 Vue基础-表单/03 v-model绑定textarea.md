
什么是：[](05_前端基础/01%20HTML%20+%20CSS/05%20高级元素/01%20高级元素的使用.md#5.7%20textarea%20的使用|textarea)

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
