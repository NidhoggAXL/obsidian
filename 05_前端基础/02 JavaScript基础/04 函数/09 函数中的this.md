# 一、创建对象

函数中是有一个this的变量，this变量在大多数情况下会指向一个对象

arguments保存的是传入的所有参数

**目前掌握两个this的判断方法:**

* 以默认的方式调用一个函数，this指向window对象;
* 通过对象调用，this指向调用的对象

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727533545000ywkcwu.png)

**情况一：对象直接调用，对象赋值调用**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727533982000rzstpm.png)


**情况二：函数赋值调用，根本逻辑还是函数的调用**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727534152000qe3gku.png)

**函数中的this在开发中的使用：**

```js
var bar = {
  name: "why",
  age: 18,
  running: function() {
	console.log(this.name)
  },
  eatting: function() {
	console.log(this.age)
  }
}

bar.running()//why
bar.eatting()//18
```

这样的好处是当我们后面进行对象的命名该改变的时候，就不需要对寒素内部进行改变，使**对象里面的属性和对象名进行分隔**，不用进行参数的传入。

**如果不使用 this 的话就是下面这段代码：**

```js
var bar = {
  name: "why",
  age: 18,
  running: function() {
	console.log(bar.name)
  },
  eatting: function() {
	console.log(bar.age)
  }
}

bar.running(bar)//why
bar.eatting(bar)//18
```

[[01 this的绑定规则|JavaScript高级this绑定]]

# 二、创建一系列对象

方法一：使用构造函数、工厂函数思想

```js
function creatStudent(name, age, height) {
  var student = {}
  student.name = name
  student.age = age
  student.height = height
  student.eating = function() {
	console.log(`${name}爱吃汉堡`)
  }
  return student
}

var student1 = creatStudent("coder",18,18.8)
console.log(student1)
console.log(typeof(student1))//Object - 对象
```

方法二：使用 this 

```js
<script>
  function Student(name,age,height) {
    this.name = name
    this.age = age
    this.height = height
    this.eating = function() {
    console.log(`${name}爱吃汉堡`)
    }
  }
  
  var student = new Student("coder",18,19.8)
  student.eating()//coder爱吃汉堡
  console.log(student)//Student - 类
  //Student {name: 'coder', age: 18, height: 19.8, eating: ƒ}
  
  console.log(typeof student)//object
</script>
```

## 2.1 认识构造函数

工厂方法创建对象有一个比较大的问题:**我们在打印对象时，对象的类型都是0bject类型**

* 但是从某些角度来说，这些对象应该有一个他们共同的类型:


我们先理解什么是构造函数?

* 构造函数也称之为构造器(constructor)，通常是我们在创建对象时会调用的函数;
* 在其他面向的编程语言里面，构造函数是存在于类中的一个方法，称之为构造方法
* 但是JavaScript中的构造函数有点不太一样，**构造函数扮演了其他语言中类的角色，**

也就是在JavaScript中，构造函数其实就是类的扮演者:

* 比如系统默认给我们提供的Date就是一个构造函数，也可以看成是一个类，
* 在ES5之前，我们都是通过function来声明一个构造函数(类)的，之后通过new关键字来对其进行调用
* 在ES6之后，JavaScript可以像别的语言一样，通过[[01 class方式定义类|class]]来声明一个类;****

> [!tip] 开发中
> 为了区分构造函数和普通函数，**构造函数使用大驼峰，普通函数使用小驼峰**


## 2.2 类和对象的关系

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727598571000jvrwyu.png)


## 2.3 JavaScript中的类（ES5）
JavaScript中的构造函数是怎么样的?

* 构造函数也是一个普通的函数，从表现形式来说，和干千万万个普通的函数没有任何区别;
* 那么如果这么一个**普通的函数被使用new操作符来调用**了，那么**这个函数就称之为是一个构造函数;**

如果一个函数被使用new操作符调用了，那么它会执行如下操作:

* 在内存中创建一个新的对象(空对象);
* 这个对象内部的`[[prototype]]`属性会被赋值为该构造函数的[[01 对象和函数的原型(prototype)|prototype]]属性
* 构造函数内部的this，会指向创建出来的新对象;
* 执行函数的内部代码(函数体代码);
* 如果构造函数没有返回非空对象，则返回创建出来的新对象，

