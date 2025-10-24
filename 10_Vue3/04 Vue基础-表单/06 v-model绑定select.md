使用的是：[[01 高级元素的使用#5.8 select 和 option 的使用|select]]

**单选：只能选中一个值**

* v-model绑定的是一个值； 
* 当我们选中option中的一个时，会将它对应的value赋值到 <mark class="hltr-orange">select</mark> 中； 

**多选：可以选中多个值** 

* v-model绑定的是一个数组； 
* 当选中多个值时，就会将选中的option对应的value添加到数组 <mark class="hltr-orange">current</mark> 中；

**select分为单选和多选：**

* 需要注意的是，这个时候绑定 v-model 是到 select 元素中，而不是option中
* select会自动检测option中的选项 value

```html
<body>
 <div id="app">
  <select class="select" v-model="selection">
   <option value="1">选项1</option>
   <option value="2">选项2</option>
   <option value="3">选项3</option>
  </select>
  <p>当前选中select是:{{ selection }}</p>

  <!-- multiple(多重的)属性表示多选,可以选中多个选项
  size属性表示显示的选项数量 -->
  <select multiple size="3" v-model="current">
   <option value="1">选项1</option>
   <option value="2">选项2</option>
   <option value="3">选项3</option>
  </select>
  <p>当前选中current是:{{ current }}</p>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data() {
    return {
     selection: '1', // 默认选中第一个选项
     current: '' // 默认选中第一个选项
    }
   }
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745937756000i5gagg.png)

