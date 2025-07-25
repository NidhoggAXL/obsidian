# 一、什么是响应式？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/175343504200063ds0i.png)

# 二、响应式函数设计

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753435089000f4kd0w.png)

# 三、响应式函数的实现watchFn

但是我们怎么区分呢？ 

* 这个时候我们封装一个新的函数watchFn； 
* 凡是传入到watchFn的函数，就是需要响应式的； 
* 其他默认定义的函数都是不需要响应式的；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753435315000lz0y65.png)


# 四、响应式依赖的收集

目前我们收集的依赖是放到一个数组中来保存的，但是这里会存在数据管理的问题： 

* 我们在实际开发中需要监听很多对象的响应式； 
* 这些对象需要监听的不只是一个属性，它们很多属性的变化，都会有对应的响应式函数； 
* 我们不可能在全局维护一大堆的数组来保存这些响应函数； 

所以我们要设计一个类，这个类用于管理某一个对象的某一个属性的所有响应式函数： 

* 相当于替代了原来的简单 reactiveFns 的数组；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753435727000koyljq.png)

```js
const obj = {
  name: 'axl',
  age:18
}

class Depend {
  constructor() {
    //构建一个数组来存储依赖函数
    this.reactiveFns = []
  }
  addDepend(fn) {
    //将依赖函数添加到数组中
    this.reactiveFns.push(fn)
  }
  //进行通知
  notify() {
    //遍历数组，执行每个依赖函数
    this.reactiveFns.forEach(fn => {
      fn()
    })
  }
}

const dep = new Depend()
function watchFn(fn) {
  //将依赖函数添加到依赖管理器中
  dep.addDepend(fn)
  fn()
}

watchFn(function() {
  console.log("foo:", obj.name)
  console.log("foo:", obj.age)
})

watchFn(function() {
  console.log("bar:", obj.age)
})

obj.name = "kobe"
console.log("---------")
//进行通知存在的依赖
dep.notify()


```
# 五、监听对象的变化

那么我们接下来就可以通过之前学习的方式来监听对象的变量： 

* 方式一：通过 Object.defineProperty的方式（vue2采用的方式）； 
* 方式二：通过new Proxy的方式（vue3采用的方式）；

我们这里先以Proxy的方式来监听：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753442481000wttrm1.png)

# 六、对象的依赖管理

我们目前是创建了一个Depend对象，用来管理对于name变化需要监听的响应函数： 

* 但是实际开发中我们会有不同的对象，另外会有不同的属性需要管理； 
* 我们如何可以使用一种数据结构来管理不同对象的不同依赖关系呢？ 

在前面我们刚刚学习过WeakMap，并且在学习WeakMap的时候我讲到了后面通过WeakMap如何管理这种响应 式的数据依赖：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753442555000r5tbio.png)

# 七、对象依赖管理的实现

我们可以写一个getDepend函数专门来管理这种依赖关系：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534530370004oyfst.png)

```js
//定义变量map保存对象的objmap
const targetMap = new WeakMap()
const getDepends = (obj, key) => {
  //obj -> 对象的映射
  let objMap = targetMap.get(obj)
  if (!objMap) {
    objMap = new Map()
    targetMap.set(obj, objMap)
  }
  
  //对象映射：{key, depend}
  let depend = objMap.get(key)
  if (!depend) {
    depend = new Depend()
    objMap.set(key, depend)
  }
  
  //返回这个depend
  return depend
}
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753453171000t55swd.png)

# 八、正确收集依赖

我们之前收集依赖的地方是在 watchFn 中： 

* 但是这种收集依赖的方式我们根本不知道是哪一个key的哪一个depend需要收集依赖； 
* 你只能针对一个单独的depend对象来添加你的依赖对象； 

那么正确的应该是在哪里收集呢？

* 应该在我们调用了Object.defineProperty的get捕获器时 
* 因为如果一个函数中使用了某个对象的key，那么它应该被收集依赖；

```js
//让局部到全局的装换
let reactiveFn = null
function watchFn(fn) {
  //fn和reactiveFn同一个引用
  //fn局部到reactiveFn外部
  reactiveFn = fn
  fn()
  //使用完后滞空，防止不变
  reactiveFn = null
}
```

```js
  //遍历对象的属性
  Object.keys(obj).forEach(key => {
    //定义变量为value
    let value = obj[key]
    Object.defineProperty(obj, key, {
      get() {
        //获取key对应的dep
        const dep = getDepends(obj, key)
        //reactiveFn有值时收集依赖
        if (reactiveFn) {
          dep.addDepend(reactiveFn)
        }
        return value
      },
      set(newValue) {
        //不要obj[key]=newValue会形成死循环(一直在set)
        value = newValue
        //获取key对应的dep
        const dep = getDepends(obj, key)
        //通知收到的依赖
        dep.notify()
      }
    })
  })
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534533510005jsqpx.png)

# 九、对Depend重构

但是这里有两个问题： 

* 问题一：如果函数中有用到两次key，比如name，那么这个函数会被收集两次； 
* 问题二：我们并不希望将添加reactiveFn放到get中，以为它是属于Dep的行为； 

所以我们需要对Depend类进行重构： 

* 解决问题一的方法：不使用数组，而是使用Set； 
* 解决问题二的方法：添加一个新的方法，用于收集依赖；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753453459000qgr6y8.png)

# 十、创建响应式对象

我们目前的响应式是针对于obj一个对象的，我们可以创建出来一个函数，针对所有的对象都可以变成响应式对象：

```js
//分装函数，让对象都可以进行响应式
function reactive(obj) {
  //遍历对象的属性
  Object.keys(obj).forEach(key => {
    //定义变量为value
    let value = obj[key]
    Object.defineProperty(obj, key, {
      get() {
        //获取key对应的dep
        const dep = getDepends(obj, key)
        //reactiveFn有值时收集依赖
        if (reactiveFn) {
          dep.addDepend(reactiveFn)
        }
        return value
      },
      set(newValue) {
        //不要obj[key]=newValue会形成死循环(一直在set)
        value = newValue
        //获取key对应的dep
        const dep = getDepends(obj, key)
        //通知收到的依赖
        dep.notify()
      }
    })
  })
  //要返回这个对象
  return obj
}
```

```js
const axl = reactive({
  name: "world",
  age: 20
})


watchFn(function () {
  console.log("foo:", axl.name)
  console.log("foo:", axl.age)
})

watchFn(function () {
  console.log("bar:", axl.age)
})
```

# 十一、总代码

```js

class Depend {
  constructor() {
    //set不可以重叠，防止收集重复
    this.reactiveFns = new Set()
  }
  addDepend(fn) {
    this.reactiveFns.add(fn)
  }
  notify() {
    this.reactiveFns.forEach(fn => {
      fn()
    })
  }
}

//定义变量map保存对象的objmap
const targetMap = new WeakMap()
const getDepends = (obj, key) => {
  //obj -> 对象的映射
  let objMap = targetMap.get(obj)
  if (!objMap) {
    objMap = new Map()
    targetMap.set(obj, objMap)
  }
  
  //对象映射：{key, depend}
  let depend = objMap.get(key)
  if (!depend) {
    depend = new Depend()
    objMap.set(key, depend)
  }
  
  //返回这个depend
  return depend
}

//让局部到全局的装换
let reactiveFn = null
function watchFn(fn) {
  //fn和reactiveFn同一个引用
  //fn局部到reactiveFn外部
  reactiveFn = fn
  fn()
  //使用完后滞空，防止不变
  reactiveFn = null
}

//分装函数，让对象都可以进行响应式
function reactive(obj) {
  //遍历对象的属性
  Object.keys(obj).forEach(key => {
    //定义变量为value
    let value = obj[key]
    Object.defineProperty(obj, key, {
      get() {
        //获取key对应的dep
        const dep = getDepends(obj, key)
        //reactiveFn有值时收集依赖
        if (reactiveFn) {
          dep.addDepend(reactiveFn)
        }
        return value
      },
      set(newValue) {
        //不要obj[key]=newValue会形成死循环(一直在set)
        value = newValue
        //获取key对应的dep
        const dep = getDepends(obj, key)
        //通知收到的依赖
        dep.notify()
      }
    })
  })
  //要返回这个对象
  return obj
}

//=============测试===============
const axl = reactive({
  name: "world",
  age: 20
})

watchFn(function () {
  console.log("foo:", axl.name)
  console.log("foo:", axl.age)
})

watchFn(function () {
  console.log("bar:", axl.age)
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753453646000alz9dw.png)


