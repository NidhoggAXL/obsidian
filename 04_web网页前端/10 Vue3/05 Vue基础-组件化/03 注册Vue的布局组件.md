# 一、注册局部组件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17461070870002p9vhx.png)

```html
<body>
 <div id="app">
  <h1-compoent></h1-compoent>
  <p-compoent></p-compoent>
 </div>

 <template id="h1-compoent-template">
  <h1>我是标题h1</h1>
 </template>
 
 <template id="p-compoent-template">
  <p>我是段落p</p>
 </template>

 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({
   // 通过data方法定义数据
   data() {},
   
   //components定义局部组件
   components: {
    // 自定义局部组件1
    'h1-compoent': {
     template: '#h1-compoent-template'
    },
    // 自定义局部组件2
    'p-compoent': {
     template: '#p-compoent-template'
    }
   }
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

> [!tip] 特别注意：
> 如果两个局部组件时同一个等级，相互之间不可以进行调用，除非在进行定义为局部组件。

# 二、两个局部组件调用

```js
//components定义局部组件
components: {
// 自定义局部组件1
'h1-compoent': {
    template: '#h1-compoent-template',

    // 再进行componets定义局部组件
    components: {
    // 在局部组件里面使用局部组件
    'p-compoent': {
    template: '#p-compoent-template'
    }
    }
}
}
```

这样就可以再 h1 局部组件里面使用 p 局部组件。

看着还是不舒服，<mark class="hltr-orange">那么可以把 局部组件整体抽取出来。</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746107999000v4d5kq.png)


