# 一、函数表达式

在JavaScript中，函数并不是一种神奇的语法结构，而是一种特殊的值

* 前面定义函数的方式，我们称之为函数的声明(Function Declaration)


还有另外一种写法是函数表达式(Function Expressions)


```js
var bar = function() {
  //语句
}

bar()
```

**注意，function 关键字后面没有函数名**

* 函数表达式允许省略函数名

> 上面的例子中 bar 是一个变量并不是一个函数名

无论函数是如何创建的，函数都是一个值(这个值的类型是一个对象-函数对象)

```js
<script>
  function foo() {}
  console.log(typeof foo)//function
</script>
```

在JavaScript开发中，我们可以将函数作为[[06 JS头等函数|头等公民]]。

# 二、函数声明vs函数表达式

在开发中，函数的声明和函数表达式有什么区别，以及如何选择呢?

首先，语法不同:

* 函数声明:在主代码流中声明为**单独的语句**的函数。
* 函数表达式:在**一个表达式中或另一个语法结构**中创建的函数。

其次，JavaScript创建函数的时机是不同的:

* 函数表达式是在**代码执行到达时**被创建，并且仅从那一刻起可用。
* 而函数声明被定义之前，它就可以被调用。
	* 这是内部算法的原故，
	* 当JavaScript 准备 运行脚本时，**首先会在脚本中寻找全局函数声明，并创建这些函数,**

```js
bar()//声明前可以调用 hello world

function bar() {
  console.log("hello world")
}
```

```js
bar()//表达式前不可调用 bar is not a function

var bar = function() {
  console.log("hello world")
}
```

开发中如何选择呢?

* 当我们需要声明一个函数时，**首先考虑函数声明语法**
* 它能够为组织代码提供更多的灵活性，因为我们可以在声明这些函数之前调用这些函数。
