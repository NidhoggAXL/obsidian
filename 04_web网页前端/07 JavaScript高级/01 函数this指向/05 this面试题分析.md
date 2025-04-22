# 一、面试题1
```js
var name = "window";

var person = {
  name: "person",
  sayName: function () {
    console.log(this.name);
  }
};

function sayName() {
  var sss = person.sayName;
  sss(); // window
  //函数之间调用 - 默认绑定
  
  person.sayName(); // person
  //对象调用 - 隐式绑定
  
  (person.sayName)(); // person
  //.的优先级很高
  //person.sayName()等价于(person.sayName)()
  //对象调用 - 隐式绑定
  
  (b = person.sayName)(); // window
  //等价域
  //b = person.sayName
  //(b)()
  //所以是一个间接引用 - window
}

sayName();
```


# 二、面试题2
```js
var name = 'window'

var person1 = {
  name: 'person1',
  foo1: function () {
    console.log(this.name)
  },
  foo2: () => console.log(this.name),
  foo3: function () {
    return function () {
      console.log(this.name)
    }
  },
  foo4: function () {
    return () => {
      console.log(this.name)
    }
  }
}
  
var person2 = { name: 'person2' }
  
person1.foo1(); //隐式绑定 - peoson1
person1.foo1.call(person2); //显式绑定 - person2

person1.foo2(); // 上层作用域 - window
person1.foo2.call(person2); // 上层作用域 - window
  
person1.foo3()(); // 默认绑定 - window
person1.foo3.call(person2)(); // 隐式绑定 - window
person1.foo3().call(person2); // 显示绑定 - person2
  
person1.foo4()(); // 隐式绑定 - prison1
person1.foo4.call(person2)(); // 上层作用域 - person2
person1.foo4().call(person2); // 上层作用域 - person1
```

**解析一：**

![[this作用域面试题]]

# 三、面试题3
```js
  
var name = 'window'
function Person (name) {
  this.name = name
  this.foo1 = function () {
    console.log(this.name)
  },
  this.foo2 = () => console.log(this.name),
  this.foo3 = function () {
    return function () {
      console.log(this.name)
    }
  },
  this.foo4 = function () {
    return () => {
      console.log(this.name)
    }
  }
}
  
var person1 = new Person('person1')
  
person1.foo1() //隐式绑定 - person1
person1.foo1.call(person2) // 显式绑定 - person2
  
person1.foo2() // 上层作用域 - person1（上层函数，person1传入）
person1.foo2.call(person2) // 上层作用域 - person1（上层函数，person1传入）
//箭头函数没有this绑定，向上层查找this
  
person1.foo3()() // 默认绑定 - window（函数直接调用）
person1.foo3.call(person2)() // 默认绑定 - window
//外层函数有 call 显式绑定 person2
//内层函数有this默认绑定，就不会向外层查找this了
person1.foo3().call(person2) // 显式绑定 - person2（内层函数显式绑定person2）
  
person1.foo4()() //隐式绑定 - person1
//内层箭头函数没有this绑定，外层查到到隐式函数this隐式绑定person1
person1.foo4.call(person2)() //上层作用域 - peison2
//内层箭头函数没有this绑定，外层显式绑定person2
person1.foo4().call(person2) //上层作用域 - person1
//内层箭头函数没有this绑定，外层隐式绑定person1
```

new操作创建对象的内存表现：

> new操作后会进行的步骤：
> 1. 创建一个空的对象
> 2. 将这个空的对象赋值给this
> 3. 执行函数体中代码
> 4. 将这个新的对象默认返回
 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1730448207000gf2m3v.png)



# 四、面试题4
```js
var name = 'window'

function Person (name) {
  this.name = name
  this.obj = {
    name: 'obj',
    foo1: function () {
      return function () {
        console.log(this.name)
      }
    },
    foo2: function () {
      return () => {
        console.log(this.name)
      }
    }
  }
}

var person1 = new Person('person1')
var person2 = new Person('person2')
  
person1.obj.foo1()() //默认调用 - Window
person1.obj.foo1.call(person2)() //默认调用 - Window
person1.obj.foo1().call(person2) //显式调用 - person2（显式调用）
  
person1.obj.foo2()() //上层作用域 - person1（隐式调用）
person1.obj.foo2.call(person2)() //上层作用域 - perons2（显式调用）
person1.obj.foo2().call(person2) //上册作用域 - person1（隐式调用）
//内层箭头函数不存在this绑定，call显式绑定无效
//外侧存在this的作用域，且this是一个隐式绑定obj
```

内存表现：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1730451366000dlyra8.png)
