# 一、函数对象的属性
我们知道JavaScript中函数也是一个对象，那么对象中就可以有属性和方法。

**属性name**：一个函数的名词我们可以通过name来访问；

```js
  <script>
    function foo() {}
    console.log(foo.name)//foo
  </script>
```

**属性length**：属性length用于**返回函数参数的个数；**

```js
  <script>
    function foo(item1, item2) {}
    console.log(foo.length)//2
  </script>
```

* length跟传入的实参没有关系，**只和形参有关**

```js
  <script>
    function foo(){}
    foo(1, 2, 3)
    console.log(foo.length)//0
  </script>
```

* 注意：rest（剩余）参数是不参与参数的个数的；

```js
  <script>
    function foo(item1, item2, ...others) {}
    console.log(foo.length)//2
  </script>
```

* 直接赋值参数也不参与

```js
  <script>
    function foo(item1, item2, item3 = 20) {}
    console.log(foo.length)//2
  </script>
```


# 二、认识arguments
arguments 是一个对应于 **传递给函数的参数** 的 **类数组(array-like)对象。**

```js
  <script>
    function foo(x, y ,z) {
      console.log(arguments)
      //Arguments(3) [10, 25, 30, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    }
    foo(10, 25, 30)
  </script>
```

arguments 之和传入的**实参有关**，和形参无关：

```js
<script>
  function foo1(name, age) {
    console.log(arguments)
    //Arguments(3) ['axl', 18, 19, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    console.log(arguments.length)//3
  }
  foo1("axl", 18, 19)
  
  function foo2(name, age, ...other) {
    console.log(arguments)
    //Arguments(4) ['axl', 18, 19, 20, callee: (...), Symbol(Symbol.iterator): ƒ]
    console.log(arguments.length)//4
    console.log(foo2.length)//2 (只和形参有关)
    console.log(other)//[19, 20]
    console.log(other.length)//2
  }
  foo2("axl", 18, 19, 20)
</script>
```

**array-like意味着它不是一个数组类型，而是一个对象类型:**

* 但是它却拥有数组的一些特性，比如说length，比如可以通过index索引来访问:
* 但是它却没有数组的一些方法，比如[[05 数组Array#8.1 filter-过滤}|filter]]、[[05 数组Array#8.2 map-映射|map]]等;

```js
<script>
  function foo(x, y ,z) {
    console.log(arguments)
    //Arguments(3) [10, 25, 30, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    console.log(foo.length)//3
    console.log(arguments[0])//10
    console.log(arguments[1])//25
    console.log(arguments[2])//30
  }

  foo(10, 25, 30)
</script>
```

**获取arguments里面的实参**

* arguments是类数组对象
* arguments是可迭代（iterator）

```js
<script>
	function foo(num1, num2) {
	  for (var num of arguments) {
		console.log(num)
	  }
	}
	
	foo(11, 22)
	//11
	//22
</script>
```

# 三、arguments转Array
在开发中，我们经常需要将arguments转成Array，以便使用数组的一些特性。

**转化方式一**：遍历arguments，添加到一个新数组中;

**转化方式二**:较难理解(有点绕)，了解即可

* 调用数组slice函数的call方法;

**转化方式三**:**ES6** 中的两个方法
* Array.from
* `[...arguments]`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731051935000qyt1w8.png)


# 四、箭头函数不绑定arguments
**箭头函数是不绑定arguments的，所以我们在箭头函数中使用arguments会去上层作用域查找:**

```js
  <script>
    var bar = () => {
      console.log(arguments)
    }
  
    bar()//arguments is not defined
  </script
```

 箭头函数不绑定arguments，bar 箭头函数内部不绑定向外层查找，查找到外层的全局也没有，就进行报错
 
* 透过上面代码，可以知道全局里面是没有arguments的

```js
  <script>
    function foo() {
      var bar = () => {
        console.log(arguments)
      }
      bar()
    }
    foo(111, 222)
    //Arguments(2) [111, 222, callee: ƒ, Symbol(Symbol.iterator): ƒ
  </script>
```

> bar 箭头函数没有arguments，就会向上层作用域查找，foo 不是箭头函数，里面就存在 arguments ，foo 调用的时候传入了 111， 222 参数到 bar 里面就打印上层作用域的arguments

# 五、函数的剩余(rest)参数 
ES6中引用了rest parameter，可以将**不定数量的参数放入到一个数组中:**

* 如果最后一个参数是`…`为前缀的，那么它会将剩余的参数放到该参数中，并且作为一个数组;

```js
  <script>
    function foo(num1, num2, ...others) {
      console.log(num1, num2)//11 22
      console.log(others)//[33, 44]
    }
    foo(11, 22, 33, 44)
  </script>
```

> 剩余参数命名时随便的，上面代码的 others 也可以命名 args

那么剩余参数和arguments有什么区别呢?

* 剩余参数只包含那些没有对应形参的实参，而 arguments 对象包含了传给函数的所有实参
* arguments对象不是一个真正的数组，而rest参数是一个真正的数组，可以进行数组的所有操作;

```js
  <script>
    function foo(num1, num2, ...others) {
      console.log(arguments)
      //Arguments(4) [11, 22, 33, 44, callee: (...), Symbol(Symbol.iterator): ƒ]
      console.log(others)
      //[33, 44]
    }
    foo(11, 22, 33, 44)
  </script>
```

> `console.log(arguments)` 打印结果时Arguments
> 且`Symbol(Symbol.iterator)`象征.迭代
> `console.log(others)` 打印结果是一个数组

* arguments是早期的ECMAScript中为了方便去获取所有的参数提供的一个数据结构，而**rest参数是ES6中提供**并且希望以此来**替代arquments的;**


