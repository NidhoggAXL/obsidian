# 一、JavaScript常见数据类型
JavaScript 中的值都具有特定的类型。

* 例如，字符串或数字。
* 我们可以将值赋值给一个变量，那么这个变量就具备了**特定的类型**
* 一个变量可以在**前一刻是个字符串，下一刻就存储一个数字;**
* 允许这种操作的编程语言，例如JavaScript，被称为“**动态类型**”(dynamically typed)的编程语言;


在 JavaScript 中有8种基本的数据类型(7 种原始类型和1种复杂类型-Object)

* Number
* String
* Boolean
* Undefined
* NuIl
* Object
* BigInt(后续了解)
* Symbol(后续了解)


# 二、typerof操作符
因为 ECMAScript 的类型系统是松散的，所以需要一种手段来确定任意变量的数据类型

* typeof 操作符就是为此而生的。

```js
var info = 12
console.log(typeof info)
```

对一个值使用 typeof 操作符会返回下列字符串之一:

* "undefined"表示值未定义:
* "boolean"表示值为布尔值:
* “string"表示值为字符串;
* “number"表示值为数值;
* "object"表示值为对象(而不是函数)或 null
* "function"表示值为函数;
* “symbol”表示值为符号;

typeof()的用法:

* 你可能还会遇到另一种语法 **:typeof(x)，它与 typeofx相同;**
* typeof是一个操作符，**并非是一个函数，()只是将后续的内容当做一个整体而已**

```js
<script>
  console.log(typeof null)//object
  console.log(typeof(null))//boject
</script>
```

