# 一、this到底指向什么？

我们先来看一个让人困惑的问题

* 定义一个函数，我们采用三种不同的方式对它进行调用,它产生了三种不同的结果

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17302799710001t8xgt.png)


这个的案例可以给我们什么样的启示呢?

* 函数在调用时，JavaScript会默认给this绑定一个值
* this的绑定和**定义的位置(编写的位置)没有关系**
* this的绑定和**调用方式以及调用的位置有关系**
* this是在**运行时被绑定**的,

## 1.1 绑定一:**默认**绑定
什么情况下使用默认绑定呢?独立函数调用。

* 独立的函数调用我们可以理解成函数没有被绑定到某个对象上进行调用;

**普通模式下：表示Window**

```js
<script>
	// 1.普通的函数被默认调用
	function fool() {
	  console.log(this)
	}
	fool()//Window
	
	//函数定义在对象中，但是独立调用
	var bar = {
	  name: "axl",
	  demo: function() {
		console.log(this)
	  }
	}
	var baz = bar.demo
	baz()//Window
</script>
```

**严格（strict）模式下：表示undefined**

```js
  <script>
    //严格模式下-strict(严格)
    "use strict"

    // 1.普通的函数被默认调用
    function fool() {
      console.log(this)
    }
    fool()//undefine

    //函数定义在对象中，但是独立调用
    var bar = {
      name: "axl",
      demo: function() {
        console.log(this)
      }
    }
    var baz = bar.demo
    baz()//undefine
  </script>
```

**在高阶函数中作为参数传入调用也是默认调用**

```js
<script>
    var bar = {
      name: "axl",
      demo: function() {
        console.log(this)
      }
    }
  
    function box(fn) {
      fn()
    }
    box(bar.demo)//Window
</script>
```
## 1. 2 绑定二:**隐式**绑定
另外一种比较常见的调用方式是通过**某个对象进行调用的:**

* 也就是它的调用位置中，是通过**某个对象发起的函数调用**。

```js
  <script>
    //bar被隐士绑定到了this上面
    function foo() {
      console.log(this)
    }
  
    var bar = {
      name: "axl",
      demo: foo
    }
  
    bar.demo()//Object
  </script>
```

```js
<script>
  function foo() {
    console.log(this)
  }
  
  var obj1 = {
    name: "obj1",
    foo: foo
  }
  
  var obj2 = {
    name: "obj2",
    obj1: obj1
  }
  
  obj2.obj1.foo()
  //{name: 'obj1', foo: ƒ}
```


```js
<script>
  function foo() {
    console.log(this)
  }
  
  var obj = {
    name: "obj",
    foo: foo
  }

  //函数赋值给bar
  var bar = obj.foo
  //赋值的bar之间调用
  bar()//Window
</script>
```
 
## 1.3 绑定三:**显示**绑定;

隐式绑定有一个前提条件:

* 必须**在调用的对象内部有一个对函数的引用**(比如一个属性);
* 如果没有这样的引用，在进行调用时，会报找不到该函数的错误;
* 正是通过这个引用，间接的将this绑定到了这个对象上:

如果我们不希望在 **对象内部** 包含这个 **函数的引用**，同时又希望在这个对象上 **进行强制调用**

### 1.3.1 call、apply

```js
  <script>
    var bar = {
      name: "axl"
    }
  
    function fool() {
      console.log(this)
    }
    //把bar显示绑定到fool函数上面
    fool.call(bar)//Object-bar
  </script>
```

JavaScript所有的函数都可以使用call和apply(应用)方法

* 第一个参数是相同的，要求传入一个对象;
	* 这个对象的作用是什么呢?就是给this准备的。
	* 在调用这个函数时，会将this绑定到这个传入的对象上。
* 后面的参数，**apply为数组，call为参数列表;**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17302916950007fa7hc.png)


```js
  <script>
    function fool(name, age) {
      console.log(this, name, age)
    }
  
    fool.apply("haha", ["axl", 18])
    //String {'haha'} 'axl' 18
  
    fool.call("hehe", "axl", 18)
    //String {'hehe'} 'axl' 18
  </script>
```

因为上面的过程，我们明确的绑定了this指向的对象，所以称之为 **显示绑定**。

### 1.3.2 bind
如果我们希望一个函数**总是**显示的绑定到一个对象上，可以怎么做呢?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1730293167000lrj79n.png)

* 使用bind方法，bind()方法创建一个新的**绑定函数(bound function，BF):**
* 绑定函数是一个 exotic function object(**怪异函数对象，ECMAScript 2015 中的术语)**

```js
  <script>
    function fool(name, age) {
      console.log(this, name, age)
    }
  
    var obj = {name: "axl"}
    var bar = fool.bind(obj, "kobe", 19)
    //bar绑定函数，把obj绑定到bar上面
    //本质还是在创建一个函数

    bar()//bar也是一个怪异函数对象
    //Object 'kobe' 19
  </script>
```
## 1.4 绑定四:**new**绑定:

JavaScript中的函数可以**当做一个类的构造函数来使用**，也就是使用new关键字。

使用new关键字来调用函数是，会执行如下的操作:

1. 创建一个全新的对象;
2. 这个新对象会被执行[[02 new、constructor|prototyp]]连接;
3. 这个新对象会绑定到函数调用的this上(this的绑定在这个步骤完成);
4. 如果函数没有返回其他对象，表达式会返回这个新对象;

```js
<script>
  function foo() {
    this.name = "axl"
    console.log(this)
  }

  var bar = new foo()//foo {name: 'axl'}
  console.log(bar)//foo {name: 'axl'}

  console.log(typeof bar)//object
  console.log(typeof foo)//function
</script>
```

进行 `new foo()` 的时候就会进行打印啦（先执行foo函数里面的代码快，才会进行 new 操作），通过赋值给 bar 可以可以看到 new 出来的是一个对象。

## 1.5 内置函数的绑定this思考
有些时候，我们会调用一些JavaScript的内置函数，或者一些第三方库中的内置函数。

* 这些内置函数会要求我们传入**另外一个函数**;
* 我们自己**并不会显示的调用这些函数**，而且**JavaScript内部或者第三方库内部会帮助我们执行,**
* 这些函数中的this又是如何绑定的呢?

setTimeout、数组的forEach、点击click

```html
<body>
  <button>点击</button>
  <script>
    setTimeout(function() {
      console.log(this)//Window
    }, 1000)
  
    var btnEl = document.querySelector("button")
    btnEl.onclick = function() {
      console.log(this === btnEl)//true
    }

    var names = ["a", "b", "c"]
    //可以默认绑定this，forEach第二参数
    var obj = {name: "axl"}
    names.forEach(function() {
      console.log(this)//name: 'axl'}
    }, obj)
    //如果没有绑定this的话，打印的this就是Window    
  </script>
</body>
```



