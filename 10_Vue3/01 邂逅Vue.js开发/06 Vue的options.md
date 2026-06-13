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

当然也可以使用[[07_JavaScript高级/08 JS ES6中实现继承/06 ES6对象的增强#^6b8366|ES6对象的增强]]写法：

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

[[07_JavaScript高级/01 函数this指向/01 this的绑定规则|JavaScript高级this绑定]]
# 四、问题二：this到底指向什么？

事实上Vue的源码当中就是对methods中的所有函数进行了遍历，并且通过bind绑定了this：<mark class="hltr-orange">这个this绑定到Vue创建的实例对象上。</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745406016000t4gchk.png)

# 五、其他属性

当然，这里还可以定义很多其他的属性，我们会在后续进行讲解： 

* 比如props[[10_Vue3/08 父子组件间通信/03 父组件传递子组件|03 父组件传递子组件]]、[[10_Vue3/03 Vue基础-Options API/01 computed计算属性使用|computed]]、[[10_Vue3/03 Vue基础-Options API/04 监听器watch选项使用|watch]]、[[10_Vue3/08 父子组件间通信/05 子组件传递父组件|emits]]、[[10_Vue3/12 Composition API/02 setup函数的基本使用|setup]]等等； 
* 也包括很多的[[10_Vue3/11 组件化额外知识/01 组件的生命周期|生命周期函数]]；


