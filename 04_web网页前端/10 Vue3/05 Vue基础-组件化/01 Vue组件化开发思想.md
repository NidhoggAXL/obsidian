# 一、认识组件化开发

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746100860000zllt1r.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746100864000a5d2u6.png)

# 二、组件化开发
**现在可以说整个的大前端开发都是组件化的天下，** 

* 无论从<mark class="hltr-orange">三大框架（Vue、React、Angular）</mark>，还是跨平台方案的 <mark class="hltr-orange">Flutter</mark>，甚至是<mark class="hltr-orange">移动端</mark>都在转向组件化开发，包括<mark class="hltr-orange">小程序的 开发</mark>也是采用组件化开发的思想。 

所以，学习组件化最重要的是<mark class="hltr-orange">它的思想</mark>，每个框架或者平台可能实现方法不同，但是思想都是一样的。

**我们需要通过组件化的思想来思考整个应用程序：** 

* 我们将一个完整的页面分成很多个组件； 
* 每个组件都用于实现页面的一个<mark class="hltr-orange">功能块</mark>； 
* 而每一个组件又可以进行细分； 
* 而组件本身又可以在多个地方进行<mark class="hltr-orange">复用</mark>；

# 三、Vue的组件化

**组件化是Vue、React、Angular的核心思想，也是我们后续课程的重点(包括以后实战项目):**

* 前面我们的createApp函数传入了一个<mark class="hltr-orange">对象App</mark>，这个对象其实本质上就是<mark class="hltr-orange">一个组件</mark>，也是我们应用程序的<mark class="hltr-orange">根组件</mark>
* 组件化提供了一种抽象，让我们可以开发出<mark class="hltr-orange">一个个独立可复用的小组件</mark>来构造我们的应用
* 任何的应用都会被抽象成一颗<mark class="hltr-orange">组件树</mark>;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17461014710006deu8g.png)

```html
<body>
 <div id="app">
  <h2>{{ message }}</h2>
 </div>
 <script src="../lib/vue.js"></script>
 <script>
  //app组件(根组件)
  const App = {
   data() {
    return {
     message: 'Hello Vue!'
    }
   }
  }

  // 创建一个Vue实例
  const app = Vue.createApp(App)

  // 通过mount方法挂载到页面上
  app.mount('#app')
 </script>
</body>
```
