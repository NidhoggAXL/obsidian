# 一、注册局部组件

**全局组件往往是在应用程序一开始就会全局组件完成**，那么就意味着如果某些组件我们并没有用到，也会一起被注册:

- 比如我们注册了三个全局组件:ComponentA、ComponentB、ComponentC;
- 在开发中我们只使用了ComponentA、ComponentB，如果ComponentC没有用到但是我们依然在全局进行了注册，那么就意味着类似于webpack这种打包工具在打包我们的项目时，依然会对其进行打包
- 这样最终打包出的JavaScript包就会有关于ComponentC的内容，用户在下载对应的JavaScript时也会增加包的大小;

所以在开发中**通常使用组件的时候采用的都是局部注册**:

- 局部注册是在需要使用到的组件中，通过components属性选项来进行注册
- 比如之前的App组件中，我们有data、computed、methods等选项了，事实上还可以有一个components选项
- 该components选项对应的是一个对象，对象中的键值对是 **组件的名称: 组件对象;**

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
> 如果两个局部组件是一个等级，相互之间不可以进行调用，除非在进行定义为局部组件。

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

这样就可以在 h1-compoent 局部组件里面使用 p-compoent 局部组件。

看着还是不舒服，<mark class="hltr-orange">那么可以把 局部组件整体抽取出来。</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746107999000v4d5kq.png)


