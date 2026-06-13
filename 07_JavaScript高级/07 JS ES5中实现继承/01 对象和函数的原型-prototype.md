# 一、认识对象原型
**JavaScript当中==每个对象都有==一个特殊的内置属性 `[[prototype]]`（隐式原型），这个特殊的对象可以指向==另外一个对象==。**

那么这个对象有什么用呢?

* 当我们通过引用对象的属性key来获取一个value时，它会触发`[[Get]]`的操作;
* 这个操作会**首先检查该对象是否有对应的属性，如果有的话就使用它**
* 如果对象中没有改属性，那么**会访问对象`[[prototype]]`内置属性指向的对象上的属性**
	* `[[prototype]]`原型里面也还有很多的对象

获取对象属性的方式有两种:

* 方式一:通过对象的proto属性可以获取到(但是这个是早期浏览器自己添加的，存在一定的兼容性问题);
* 方式二:通过 Object.getPrototypeOf 方法可以获取到;

```js
<script>
  var obj = {
    name: "axl",
    age: 19
  }
  
  console.log(obj.__proto__)
  console.log(Object.getPrototypeOf(obj))
  console.log(obj.__proto__ === Object.getPrototypeOf(obj))
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/173123192100075zaio.png)


# 二、函数的显式原型
==所有的函数都有==**一个prototype的属性(注意:不是proto)**

```js
<script>
  function foo() {}
  console.log(foo.prototype)
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731232633000ajkeza.png)

> [!tip] 重点理解
> * 它是一个函数，才有了prototype这个特殊的属性
> * 而不是它是一个对象，所以才有了这个特殊的属性

