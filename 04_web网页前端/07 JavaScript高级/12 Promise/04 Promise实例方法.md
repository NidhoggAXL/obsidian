# 一、then方法-接受两个参数

then方法是Promise对象上的一个方法（**实例方法**）： 

* 它其实是放在Promise的原型上的 Promise.prototype.then 

then方法接受两个参数： 

* **fulfilled(兑现)的回调函数**：当状态变成fulfilled时会回调的函数； 
* **reject(拒绝)的回调函数**：当状态变成reject时会回调的函数；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732429552000s7p2jm.png)

# 二、then方法-多次调用
一个Promise的then方法是可以**被多次调用**的： 

* 每次调用我们都可以传入对应的fulfilled回调； 
* 当Promise的状态变成fulfilled的时候，这些回调函数都会被执行；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732429614000mf7xlg.png)

# 三、then方法-返回值
then方法本身是有返回值的，它的**返回值是一个Promise**，所以我们可以进行如下的链式调用： 

```js
promis.then().then().then().catch()
```

> 但是then方法返回的Promise到底处于什么样的状态呢？

Promise有三种状态，那么这个Promise处于什么状态呢？ 

* 当then方法中的回调**函数本身在执行的时候**，那么它处于[[03 Promise状态变化|pending]]状态； 
* 当then方法中的回调函数返回一个结果时，那么它处于[[03 Promise状态变化|fulfilled]]状态，并且会将**结果作为resolve的参数**；
	* 情况一：返回一个普通的值； 
	* 情况二：返回一个Promise； 
	* 情况三：返回一个thenable值；
* 当then方法抛出一个异常时，那么它处于[[03 Promise状态变化|reject]]状态；

```js
<script>
  const p = new Promise((resolve, reject) => {
    resolve("p中的resolve")
  })
  
  const promis = new Promise((resolve, reject) => {
    resolve("aaa")
  })
  
  promis.then((res) => {
    console.log("第一次回调的res",res)
    //第一次回调的res aaa
  
    //1.情况一：返回普通值
    return "bbb"
  }).then((res) => {
    console.log("第二次回调的res",res)
    //第二次回调的res bbb
  
    //2.情况二：返回一个promis
    return p
  }).then((res) => {
    console.log("第三次回调的res",res)
    //第三次回调的res p中的resolve
  
    //3.情况三：放回一个thenable
    return {
      name: "axl",
      then: () => {
        console.log("thenable里面的then")
      }
    }
  }).then((res) => {
    console.log("第三次回调res",res)
    //thenable里面的then
  })
</script>
```


# 四、catch方法 – 多次调用
catch方法也是Promise对象上的一个方法（实例方法）：

* 它也是放在Promise的原型上的 Promise.prototype.catch 

一个Promise的catch方法是可以被多次调用的： 

* 每次调用我们**都可以传入对应的reject回调**； 
* 当**Promise的状态变成reject的时候，这些回调函数都会被执行；**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732433271000rd0x7c.png)


# 五、catch方法-返回值
事实上catch方法也是会返回一个Promise对象的，所以catch方法后面我们可以继续调用then方法或者catch方法： 

```js
<script>
  const promis = new Promise((resolve, reject) => {
    resolve("promis回调")
  })
  
  promis.catch((err) => {
    console.log("第一次回调：", err)
  }).then((res) => {
    console.log("成功的res：" ,res)
    //成功的res： promis回调
  })
</script>
```

```js
<script>
  const promis = new Promise((resolve, reject) => {
    reject("promis失败")
  })
  
  promis.catch((err) => {
    console.log("第一次回调：", err)
    //第一次回调： promis失败
  }).catch((err) => {
    console.log("第二次回调" ,err)
  })
</script>
```

那么如果我们希望后续继续执行catch，那么需要抛出一个异常：

```js
<script>
  const promis = new Promise((resolve, reject) => {
    reject("promis失败")
  })
  
  promis.catch((err) => {
    console.log("第一次回调：", err)
    //第一次回调： promis失败
    throw new Error("error message")
  }).catch((err) => {
    console.log("第二次回调" ,err)
    //第二次回调 Error: error message
  })
</script>
```

> 后续执行的 catch 中，会把 Error 里面的错误在 cath 回调的时候，把 Error 传入 cath 的形参里面。

# 六、finally方法
finally是在ES9（ES2018）中新增的一个特性：表示无论Promise对象无论变成fulfilled还是rejected状态，最终都会被执行 的代码。

finally方法是不接收参数的，因为无论前面是fulfilled状态，还是rejected状态，它都会执行。


```js
<script>
  const promis = new Promise((resolve, reject) => {
    resolve("haha")
  })
  
  promis.then((res) => {
    console.log(res)//haha
  }).catch((err) => {
    console.log(err)
  }).finally(() => {
    console.log("finally执行")//finally执行
  })
</script>
```


