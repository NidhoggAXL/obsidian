# 一、注册组件的方式

如果我们现在有一部分**内容（模板、逻辑等）**，我们希望将这部分内容抽取到一个**独立的组件**中去维护，这个时候如何注册一个 **组件呢？** 

先从简单的开始谈起，比如下面的模板希望抽离到一个单独的组件：

```html
<h2>{{ title }}</h2>
<p>{{ message }}</p>
```

**注册组件分成两种：** 

* <mark class="hltr-orange">全局组件</mark>：在任何其他的组件中都可以使用的组件； 
* <mark class="hltr-orange">局部组件</mark>：只有在注册的组件中才能使用的组件；

# 二、注册全局组件

我们先来学习一下全局组件的注册： 

* 全局组件需要使用我们全局创建的<mark class="hltr-orange">app来注册组件</mark>； 
* 通过<mark class="hltr-orange">component方法</mark>传入<mark class="hltr-orange">组件名称、组件对象</mark>即可注册一个全局组件了； 
* 之后，我们可以在<mark class="hltr-orange">App组件的template中</mark>直接使用这个<mark class="hltr-orange">全局组件</mark>：

```js
app.component(组件名词, 组件对象)
```

```html
<body>
 <div id="app">
  //使用组件，在app根组件下
  <my-compoent></my-compoent>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({})

  // 自定义一个组件
  app.component('my-compoent', {
   template: '<h2>我是自定义组件</h2>'
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

但是我们根组件会有不同，根组件就不需要使用到 createApp 里面，使用 template 就可以创建 <mark class="hltr-orange">标签的元素</mark>，这里也可以把 html 内容抽取出来。

```html
<body>
 <div id="app">
  <!-- 使用组件 -->
  <my-compoent></my-compoent>
 </div>

 <!-- 在 id="app" 之外创建模板 -->
 <template id="my-compoent-template">
  <h2>我是自定义组件</h2>
 </template>
 
 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({})

  // 自定义一个组件
  app.component('my-compoent', {
   // 通过template属性引入模板
   //在 id="my-compoent-template"的template模板中定义组件的结构
   template: '#my-compoent-template'
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

> [!tip]
> 注意my-compoent的模板实在 `id="app"` 之外定义的模板

# 三、全局组件的逻辑

组件本身也可以有自己的代码逻辑： 比如自己的data、computed、methods等等

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746105274000mccj99.png)

# 四、全局组件的特点

<mark class="hltr-orange">只要注册的是全局组件，就可以在任意的 template 中使用：</mark>

* 其中根组件 id="app" 默认就是一个 template 模板

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746106246000laju3o.png)

```html
<body>
 <div id="app">
  <!-- 在根组件里面使用h1组件 -->
  <h1-compoent></h1-compoent>
 </div>

 <template id="h1-compoent-template">
  <h1>我是标题h1</h1>
  <!-- 在h1组件里面使用p的组件 -->
  <p-compoent></p-compoent>
 </template>

 <template id="p-compoent-template">
  <p>我是段落p</p>
 </template>

 <script src="../lib/vue.js"></script>
 <script>
  // 创建一个Vue实例
  const app = Vue.createApp({})

  // 自定义全局组件1
  app.component('h1-compoent', {
   template: '#h1-compoent-template'
  })

  // 自定义全局组件2
  app.component('p-compoent', {
   template: '#p-compoent-template'
  })

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746106472000tn6leo.png)


# 五、组件的名称

在通过 app.component 注册一个组件的时候，第一个参数是组件的名称，定义组件名的方式有两种：

**方式一：使用kebab-case（短横线分割符）** 

* 当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 `<my-cpnponent-name>`；

```js
app.component('my-component-name', {})
```

**方式二：使用PascalCase（驼峰标识符）** 

* 当使用 PascalCase (<mark class="hltr-orange">首字母大写命名</mark>) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。 
* 也就是说`<my-component-name>` 和 `MyComponentName` 都是可接受的；

```js
app.component('MyComponentName', {})
```


