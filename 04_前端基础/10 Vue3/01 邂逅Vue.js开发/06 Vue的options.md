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

当然也可以使用[[06 ES6对象的增强#^6b8366|ES6对象的增强]]写法：

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

[[01 this的绑定规则|JavaScript高级this绑定]]
# 四、问题二：this到底指向什么？

事实上Vue的源码当中就是对methods中的所有函数进行了遍历，并且通过bind绑定了this：<mark class="hltr-orange">这个this绑定到Vue创建的实例对象上。</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745406016000t4gchk.png)

# 五、其他属性

当然，这里还可以定义很多其他的属性，我们会在后续进行讲解： 

* 比如props[[03 父组件传递子组件]]、[[01 computed计算属性使用|computed]]、[[04 监听器watch选项使用|watch]]、[[05 子组件传递父组件|emits]]、[[02 setup函数的基本使用|setup]]等等； 
* 也包括很多的[[01 组件的生命周期(重点)|生命周期函数]]；


