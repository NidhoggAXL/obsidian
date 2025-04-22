# 一、Reflect的作用
Reflect也是ES6新增的一个API，它是一个**对象**，字面的意思是反射。

那么这个Reflect有什么用呢？ 

* 主要提供了很多操作JavaScript对象的方法，有点像Object中操作对象的方法； 
* 比如Reflect.getPrototypeOf(target)类似于 Object.getPrototypeOf()； 
* 比如Reflect.defineProperty(target, propertyKey, attributes)类似于Object.defineProperty() ；

如果我们有Object可以做这些操作，那么**为什么还需要有Reflect这样的新增对象呢？** 

* 这是因为在早期的ECMA规范中没有考虑到这种对 **对象本身** 的操作如何设计会更加规范，所以将这些API放到了Object上面； 
* 但是Object作为一个构造函数，这些操作实际上放到它身上**并不合适**； 
* 另外还包含一些类似于 **in、delete操作符**，让JS看起来是**会有一些奇怪**的； 
* 所以在ES6中新增了Reflect，让我们这些操作都集中到了Reflect对象上；
* 另外在使用[[02 Proxy(代理）类|Proxy]]时，可以做到**不操作原对象**；

那么Object和Reflect对象之间的API关系，可以参考MDN文档： https://developer.mozilla.org/zhCN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/Comparing_Reflect_and_Object_methods

# 二、Reflect的常见方法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732195901000jb3bw3.png)


# 三、Reflect的使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732196742000cumaep.png)

> [!tip] 为什么会说不在直接操作源对象呢？看下面这段代码

```js
<script>
  const obj = {
    name: "axl",
    age: 18
  }
  
  const objProxy = new Proxy(obj, {
    set: function(target, key, newValue) {
      console.log(target === objProxy)//false
      console.log(target === obj)//true
      target[key] = newValue
    }
  })
  
  objProxy.name = "kaobe"
</script>
```

# 四、Receiver的作用
我们发现在使用getter、setter的时候有一个**receiver的参数**，它的作用是什么呢？ 

* 如果我们的源对象（obj）有**setter、getter的访问器属性，那么可以通过receiver来改变里面的this**；


```js
<script>
  const obj = {
    _name: "axl",
    set name(newName) {
      console.log("obj里面的", this)//this默认obj
      this._name = newName
    }
  }
  
  const objProxy = new Proxy(obj, {
    set: function(target, key, value) {
      console.log(`监听：${key}进行set改变`)
      Reflect.set(target, key, value)
    }
  })
  
  objProxy.name = "mba"
  //监听：name进行set改变
  //obj里面的 {_name: 'axl'}
</script>
```

上面代码的运行顺序来看一下图片：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/173219929300001fh4d.png)

根据打印结果来判断的话，obj 只发生了一次改变。

**但是我们上面的代码中，`name`发生了改变，同时`_name`也是发生了改变。**

Proxy是一个代理的，实质还是对obj创建了一个监听的对象 objProxy 代理，而当 obj 里面的name发生改变的时候，是 obj 本身发生了改变并不是 代理发生了改变，所以代理就会监听不到。**（代理对象 objProxy 引起的 obj 本身发生改变）**

**上面从情况就要使用到 Receive 来改变 obj 里面的 thsi**

```js
<script>
const obj = {
  _name: "axl",
  set name(newName) {
    console.log("obj里面的", this)//this默认obj
    this._name = newName
  }
}
  
const objProxy = new Proxy(obj, {
  set: function(target, key, value, receiver) {
    console.log(`监听：${key}进行set改变`)
    console.log(receiver)
    //set 方法传入 receiver 把 objProxy 传入进去
    Reflect.set(target, key, value, receiver)
  }
})
  
objProxy.name = "mba"
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732263635000950dvy.png)

这样就可以对 obj 不管是自身的改变还是代理对象引起发生的改变，都可以进行监听。

# 五、Reflect Construct
首先：通过前面的知识，如果在一个代码块里面执行另一个代码块的代码如何执行？

[[01 this的绑定规则#1.3.1 call、apply|call、apply]]

```js
<script>
  function Persong(name, age) {
    this.name = name
    this.age =age
  }

  function Student(name, age){
    //想在 Student 里面执行 Persong 里面的代码
    Persong.call(this, name, age)
  }
  
  const stu = new Student("axl", 18)
  console.log(stu)//Student {name: 'axl', age: 18}
  console.log(stu.__proto__ === Student.prototype)//true
</script>
```

如果使用 Reflect Construct 的话：

```js
<script>
  function Persong(name, age) {
    this.name = name
    this.age =age
  }
  
  function Student(name, age){
    //想在 Student 里面执行 Persong 里面的代码
  }
  
  const stu = Reflect.construct(Persong, ["axl", 18], Student)
  console.log(stu)//Student {name: 'axl', age: 18}
  console.log(stu.__proto__ === Student.prototype)//true
</script>
```

