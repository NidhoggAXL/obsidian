# 一、再看new操作符
讲过new关键字的步骤如下： [[01 this的绑定规则#一、this到底指向什么？#1.4 绑定四 **new**绑定|new]]

* 在内存中创建一个新的对象（空对象）； 
* 这个对象内部的`[[prototype]]`（隐式原型）属性会被赋值为该构造函数的prototype（显式属性）属性；
* 把函数内部的this指向这个新的对象
* 执行函数内部的代码
* 如果没有返回值，把这个新对象返回

那么也就意味着我们通过**Person构造函数**创建出来的所有对象的隐式原型`[[prototype]]`（隐式原型）属性都指向构造函数Person.prototype(显式原型）：

**先看如果不使用原型的代码：**

```js
<script>
  function Person(name, age, height) {
    this.name = name
    this.age = age
    this.height = height
    this.running = function() {
      console.log(this.name + "running")
    }
  }
  
  var stu1 = new Person("axl", 18, 18.8)
  var stu2 = new Person("mba", 18, 18.8)
  var stu3 = new Person("nba", 18, 18.8)
  
  console.log(stu1.running === stu2.running)//false
</script>
```

> 看上面的代码，共同创建了3个对象，这个时候我们来看代码，会发现 **running** 这个方法我们也创建了 3 次。
> 每一次都是再次创建了一个 running 方法，可以看到后面 `console.log`是false，这样的操作会浪费性能。

**再看使用原型的代码：**

```js
<script>
  function Person(name, age, height) {
    this.name = name
    this.age = age
    this.height = height
  }
  
  //函数的函数原型prototype(显式原型)设置属性running
  Person.prototype.running = function() {
    console.log(this.running + "running")
  }
  
  var stu1 = new Person("axl", 18, 18.8)
  var stu2 = new Person("mba", 18, 18.8)
  var stu3 = new Person("nba", 18, 18.8)
  
  console.log(stu1.running === stu2.running)//true
</script>
```


> 上面的代码在函数原型prototype（显式原型）设置了属性 running。
> 
> 当我们使用 new 构造函数调用的时候会把函数的函数原型prototype（显式原型）赋值给 new 创建出来对象的对象原型 `__proto__`(`[[prototype]])`隐式原型
> 
> 后面我们在调用的话`stu1.running()`，可以知道 stu1 是一个对象，对象有隐式原型，running 这个方法在`[[prototype]]`(隐式原型)里面，就可以找到使用。
> * 先在自己属性查找，没有就去自己的原型里面查找
> 
> 这个方法在对象原型里面就设置了一次，每一个对象的隐式原型**都是一样（true）**。这样就不用对每一个对象设置 running 方法。**省略了空间**。



# 二、constructor(构造器)属性
事实上原型对象上面是有一个属性的:constructor

* 默认情况下原型上都会添加一个属性叫做constructor，这个constructor指向当前的函数对象;

```js
<script>
  function Person() {}

  //函数的prototype（显式原型）中constructor属性指向当前函数
  console.log(Person.prototype.constructor)//ƒ(函数) Person() {}
  console.log(Person.name)//Person
  
  //以构造函数创建对象
  var p1 = new Person()
  //对象的__proto__(隐式原型)中constructor属性指向构造当前对象的函数
  console.log(p1.__proto__.constructor)//ƒ(函数) Person() {}
  console.log(p1.__proto__.constructor.name)//Person
  console.log(p1.__proto__.constructor === Person)//true
</script>
```


# 三、函数原型内存表现
**代码初始化：**

```js
<script>
  function Person(name, age) {
    this.name = name
    this.age = age
  }
  
  Person.prototype.running = function() {
    console.log(this.name + "running")
  }

  p1 = new Person("why", 18)
  p2 = new Person("kobe", 30)
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731292114000yen4xp.png)

**添加属性：**

```js
<script>
  function Person(name, age) {
    this.name = name
    this.age = age
  }
  
  Person.prototype.running = function() {
    console.log(this.name + "running")
  }
  
  p1 = new Person("why", 18)
  p2 = new Person("kobe", 30)
  
  Person.prototype.address = "中国"
  p2.__proto__.info = "中国很美丽！"
  
  p2.isAdmin = true
  console.log(p2.isAdmin)//true
  console.log(p2.address)//中国
  console.log(p1.info)//中国很美丽

  p1.height = 18.8
  p1.address = "广州市"
  console.log(p1.address)//广州市
  console.log(p1.info)//中国很美丽
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731292558000t5857f.png)

# 四、重写原型对象

如果我们需要在原型上添加过多的属性，通常我们会重写整个原型对象：

```js
<script>
  function Person(name, age) {
    this.name = name,
    this.age = age
  }
  
  // Person.prototype.height = 18.8
  // Person.prototype.running = function() {
  //   console.log(this.name + "running")
  // }

  //在原型添加多个属性可以使用重组原型
  Person.prototype = {
    height: 18.8,
    running: function() {
      console.log(this.name + "running")
    },
  }

  console.log(Person.prototype.constructor === Person)//false
  console.log(Person.prototype.constructor)
  //ƒ Object() { [native code] }
</script>
```


每创建一个函数, 就会同时创建它的prototype对象, 这个对象也会自动获取constructor属性； 

* 而我们这里相当于给prototype重新赋值了一个对象, 那么这个新对象的constructor属性, 会**指向Object对象构造函数, 而不是 Person 构造函数了**

# 五、原型对象的constructor
如果希望constructor指向Person，那么可以手动添加： 

上面的方式虽然可以, 但是也会造成constructor的[[01 Object.defineProperty#3.1 数据属性描述符|Enumerable]]特性被设置了true. 

* 默认情况下, 原生的constructor属性是**不可枚举**的. 

```js
<script>
  function Person(name, age) {
    this.name = name,
    this.age = age
  }
  
  Person.prototype.height = 18.8
  Person.prototype.running = function() {
    console.log(this.name + "running")
  }
  
  console.log(Object.keys(Person.prototype))
  //['height', 'running']
</script>
```

* 如果希望解决这个问题, 就可以使用我们前面介绍的Object.defineProperty()函数了.

```js
<script>
  function Person(name, age) {
    this.name = name,
    this.age = age
  }
  
  console.log(Object.getOwnPropertyDescriptor(Person.prototype, "constructor"))
  //{writable: true, enumerable: false, configurable: true, value: ƒ}
  
  Person.prototype = {
    height: 18.8,
    running: function() {
      console.log(this.name + "running")
    },
    constructor: Person
  }
  
  Object.defineProperty(Person.prototype, "constructor", {
    writable: true,
    enumerable: false,
    configurable: true,
  })
  
  console.log(Object.getOwnPropertyDescriptor(Person.prototype, "constructor"))
  //{writable: true, enumerable: false, configurable: true, value: ƒ}
</script>
```

