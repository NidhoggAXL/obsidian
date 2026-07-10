# 一、data属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745404320000sjwda8.png)

```js
export default {
 data: function () {
  return {
   count: 100,
  }
 }
}
```

当然也可以使用[](12%20ES6对象的增强.md#^6b8366|ES6对象的增强)写法：

```js
export default {
 data() {
  return {
   count: 100,
  }
 }
}
```
# 二、methods属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745405789000qvaet1.png)

```js
export default {
 data() {
  return {
   count: 100,
  }
 },
 methods: {
  add() {
   this.count++
  },
  sub() {
   this.count--
  }
 }
}
```
# 三、问题一：不能使用箭头函数？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745405997000b1lmfq.png)

[JavaScript高级this绑定](07_JavaScript高级/01%20函数this指向/01%20this的绑定规则.md)
# 四、问题二：this到底指向什么？

事实上Vue的源码当中就是对methods中的所有函数进行了遍历，并且通过bind绑定了this：<mark class="hltr-orange">这个this绑定到Vue创建的实例对象上。</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745406016000t4gchk.png)

# 五、其他属性

当然，这里还可以定义很多其他的属性，我们会在后续进行讲解： 

* 比如props[03 父组件传递子组件](10_Vue3/08%20父子组件间通信/03%20父组件传递子组件.md)、[computed](10_Vue3/03%20Vue基础-Options%20API/01%20computed计算属性使用.md)、[watch](10_Vue3/03%20Vue基础-Options%20API/04%20监听器watch选项使用.md)、[emits](10_Vue3/08%20父子组件间通信/05%20子组件传递父组件.md)、[setup](10_Vue3/12%20Composition%20API/02%20setup函数的基本使用.md)等等； 
* 也包括很多的[生命周期函数](10_Vue3/11%20组件化额外知识/01%20组件的生命周期.md)；


