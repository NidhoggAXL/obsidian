# 一、认识class类
我们会发现，按照前面的构造函数形式创建类，不仅仅和编写普通的函数过于相似，而且代码并不容易理解。 

* 在ES6（ECMAScript2015）新的标准中使用了class关键字来直接定义类； 
* 但是类本质上依然是前面所讲的构造函数、原型链的语法糖而已； 
* 所以学好了前面的构造函数、原型链更有利于我们理解类的概念和继承关系； 

那么，如何使用class来定义一个类呢？ 

* 可以使用两种方式来声明类：**类声明和类表达式；**

```js
<script>
  //类声明
  class Perong {}
  
  //类表达式
  var Person = class {}
</script>
```

# 二、类和构造函数的异同
我们来研究一下类的一些特性:你会发现它和我们的构造函数的特性**其实是一致的;**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17315072270000ti3fu.png)

# 三、类的构造函数
如果我们希望在创建对象的时候给类传递一些参数，这个时候应该如何做呢？ 

* 每个类都可以有一个**自己的构造函数（方法）**，这个方法的名称是固定的**constructor**； 
* 当我们通过**new操作符**，操作一个类的时候会**调用这个类的构造函数constructor；** 
* 每个类**只能有一个构造函数，如果包含多个构造函数，那么会抛出异常；**

当我们通过new关键字操作类的时候，会调用这个constructor函数，并且执行如下操作： 

* 在内存中创建一个新的对象（空对象）； 
* 这个**对象内部的`[[prototype]]`（显式属性）属性会被赋值为该类的`prototype`（隐式原型）属性；** 
* 构造函数内部的this，会指向创建出来的新对象； 
* 执行构造函数的内部代码（函数体代码）； 
* 如果构造函数**没有返回非空对象**，则返回创建出来的新对象；

```js
<script>
  class Persong {
    //类中的构造函数
    constructor(name, age) {
      this.name = name
      this.age = age
    }
  }

  var stu = new Persong("axl", 18)
  console.log(stu)
  //Persong {name: 'axl', age: 18}
</script>
```


# 四、类的实例方法
在上面我们定义的属性都是直接放到了this上，也就意味着它是放到了创建出来的新对象中： 

* 在前面我们说过对于实例的方法，我们是希望放到原型上的，这样可以被多个实例来共享； 
* 这个时候我们可以直接在类中定义；


```js
<script>
  class Persong {
    //类的构造函数
    //当我们通过new关键字调用一个Person类时，
    //默认调用class中的constructor方法
    constructor(name, age) {
      this.name = name
      this.age = age
    }
  
    //类的示例方法
    //实际就是在 Persong.prototype 上面进行定义
    running() {
      console.log("running")
    }
    eatting = () => {
      console.log("eatting")
    }
  }
  
  var stu = new Persong("axl", 18)
  console.log(stu)//Persong {name: 'axl', age: 18
  stu.running()//running
</script>
```


# 五、类的访问器方法

对象访问器方法的编写：

```js
<script>
  var obj = {
    name: "axl"
  }

  Object.defineProperty(boj, "name", {
    enumerable: false,
    set: function() {
      console.log("进行了设置")
    }
  })
  obj.name = "mba"//进行了设置
</script>
```

> 只能对 obj 对象中的 name 进行监听。

类的访问器方法的编写：

```js
<script>
  class Person {
    constructor(name) {
      this._name = name
    }
  
    set name(value) {
      console.log("设置name")
      this._name = value
    }
  
    get name() {
      console.log("获取name")
      return this._name
    }
  }
  
  var p1 = new Person("axl")
  console.log(p1)//Person {_name: 'axl'}
  p1.name = "coder"//设置name
  console.log(p1.name)//获取name coder
  
  var p2 = new Person("mba")
  console.log(p2.name)//获取name mba
</script>
```

> [!tip] 每个传入的 name 都可以进行监听，这就是比起 [[01 Object.defineProperty|对象访问器]] 的好处，每一个对象都是可以进行监听的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731571328000xa5b0j.png)

# 六、类的静态方法

静态方法通常用于定义直接使用类来执行的方法，不需要有类的实例，使用static关键字来定义：

```js
<script>
  class Person {
    constructor(age) {
      this.age = age
    }
  
    //对象的类方法也是类的静态方法
    static create() {
      //回调了 Person 类
      return new this(Math.floor(Math.random() * 100))
    }
  }
  
  var p1 = new Person(18)
  console.log(p1)//18
  //Person 调用，create里面的this指向Person
  var a = Person.create()
  console.log(a)//100以内的随机值
</script>
```



