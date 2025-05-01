目前我们在前面的案例中**大部分的值**都是**在template中固定好的:**

* 比如gender的两个输入框值male、female;
* 比如hobbies的三个输入框值basketball、football、tennis;

在真实开发中，我们的**数据可能是来自服务器**的，那么我们就可以先将值**请求下来，** 绑定到data返回的对象中，再通过v-bind来进行值的绑定，这个过程就是值绑定。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746087878000nalq4c.png)

```html
<body>
 <div id="app">
  //数据内容来 data 里面的数据
  <template v-for="item in allHobbys" :key="item.id">
   <label :for="item.id">
    <input :id="item.id" type="checkbox" v-model="hobbys" :value="item.name" />{{ item.text }}
   </label>
  </template>
  <h2>爱好如下：{{ hobbys }}</h2>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data() {
    return {
     hobbys: [], // 选中的爱好
     allHobbys: [
      { id: 1, name: '篮球' , text: '篮球' },
      { id: 2, name: '足球' , text: '足球' },
      { id: 3, name: '乒乓球' , text: '乒乓球' },
      { id: 4, name: '羽毛球' , text: '羽毛球' },
      { id: 5, name: '游泳' , text: '游泳' }
     ],
    }
   }
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```


