# 一、认识ES6的继承
在ES6中新增了使用extends关键字，可以方便的帮助我们实现继承：

```js
<script>
  class Person {
    constructor(name, age) {
      this.name = name
      this.age = age
    }
    runnin() {
      console.log("running")
    }
  }
  
  class Student extends Person {
    constructor(name, age, sno ,score) {
      super(name,age)
      this.sno = sno
      this.score = score
    }
    eatting() {
      console.log("eatting")
    }
  }
  
  var stu = new Student("axl", 18, 100, 90)
  console.log(stu)
</script>
```

# 二、super关键字
发现在上面的代码中我使用了一个super关键字，这个super关键字有不同的使用方式： 

Class为我们的方法中还提供了super关键字:

* 执行 super.method(..) 来调用一个父（超类）类方法。method - 方法
* 执行 super(...) 来调用一个父类 constructor(只能在我们的 constructor 中)


>[!warning] 在子（**派生**）类的构造函数中使用this或者返回默认对象之前，**<mark class="hltr-orange">必须</mark>先通过super调用父类的构造函数！** 

**super的使用位置有三个**：子类的构造函数、实例方法、静态方法；

调用子类的构造函数：就是上面是用super的地方，调用Person中的constructor

调用父类的示例方法和静态方法：

```js
<script>
  class Person {
    running() {
      console.log("running")
    }
    static eatting() {
      console.log("eatting")
    }
  }
  
  class Student extends Person {
    // 子类对父类的方法不满意（继承过来的实例方法）
    //重写实现称为重写（父类方法的重写）
    running() {
      console.log("人是两条腿")
      super.running()
    }
  
    //静态方法和示例方法一样可以重写
    static eatting() {
      super.eatting()
      console.log("apple")
    }
  }
  
  var stu = new Student()
  stu.running()
  //人是两条腿
  //running

  Student.eatting()//eatting apply
</script>
```

# 三、继承内置类

我们也可以让我们的类继承自内置类，比如Array：

```js
<script>
  class AxlArray extends Array {
    //获取数组示例最后一个数据
    lastItem() {
      return this[this.length - 1]
    }
  }
  
  var arr = new AxlArray(10, 20, 30, 40)
  console.log(arr.lastItem())//40
</script>
```


# 四、类的混入mixin（了解）

**JavaScript的类只支持单继承**:也就是只能有一个父类

* 那么在开发中我们我们需要在一个类中添加更多相似的功能时，应该如何来做呢?
* 这个时候我们可以使用混入(mixin);

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734442216000ruxlaw.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734442306000y56tly.png)



