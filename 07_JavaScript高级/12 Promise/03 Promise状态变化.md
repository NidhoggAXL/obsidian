# 一、Promise的代码结构
看一下Promise代码结构：

```js
<script>
  const promis = new Promise((resolve, reject) => {
    //1. pending 待定状态
    console.log("111")
    console.log("222")
  
    //2.fulfilled 以兑现
    resolve()
  
    //3. rejected 已拒绝
    reject()
  })
  
  promis.then( count => {
    console.log("成功的回调")
  })
  promis.catch( count => {
    console.log("失败的回调")
  })
</script>
```


上面Promise使用过程，我们可以将它划分成三个状态： 

* 待定（**pending**）: 初始状态，既没有被兑现，也没有被拒绝； ✓ 当执行executor中的代码时，处于该状态； 
* 已兑现（**fulfilled**）: 意味着操作成功完成； ✓ 执行了resolve时，处于该状态，Promise已经被兑现； 
* 已拒绝（**rejected**）: 意味着操作失败； ✓ 执行了reject时，处于该状态，Promise已经被拒绝；

# 二、Executor
Executor是在创建Promise时需要传入的一个回调函数，这个回调函数会被**立即执行，并且传入两个参数：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17324280680009xxfnh.png)


通常我们会在Executor中确定我们的Promise状态： 

* 通过 **resolve**，可以兑现（**fulfilled**）Promise的状态，我们也可以称之为**已决议**（**resolved**）； 
* 通过 **reject**，可以拒绝（**rejected**）Promise的状态；


这里需要注意：一旦状态被确定下来，Promise的状态会被 锁死，该Promise的状态是不可更改的 

* 在我们**调用resolve**的时候，如果**resolve传入的值本身不是一个Promise**，那么会将该Promise的状态变成 **兑现（fulfilled）**； 
* 在之后**我们去调用reject时，已经不会有任何的响应了**（<mark class="hltr-orange">并不是这行代码不会执行，而是无法改变Promise状态</mark>）；

# 三、resolve不同值的区别（理解）
**情况一**：如果resolve传入一个**普通的值或者对象**，那么**这个值会作为then回调的参数；**

```js
<script>
  const promis = new Promise((resolve, reject) => {
    resolve({name: "axl"})
  })
  
  promis.then(res => {
    console.log("获取res的值",res)
    //获取res的值 {name: 'axl'}
  })
</script>
```

**情况二**：如果resolve中传入的是**另外一个Promise**，那么**这个新Promise会决定原Promise的状态**： 

```js
<script>
  const p = new Promise((resolve, reject) => {
    resolve("p里面的res")
  })
  
  const promis = new Promise((resolve, reject) => {
    resolve(p)
  })
  
  promis.then(res => {
    console.log("获取res的值",res)
    //获取res的值 p里面的res
  })
</script>
```

**情况三**：如果resolve中传入的是**一个对象**，并且这个对象**有实现then方法**，那么**会执行该then方法**，并且根据**then方法的结 果来决定Promise的状态：**

```js
<script>
  const promis = new Promise((resolve, reject) => {
    resolve({
      name: "axl",
      then: () => {
        console.log("对象里面的then方法")
      }
    })
  })
  
  promis.then(res => {
    console.log("获取res的值",res)
    //对象里面的then方法
  })
</script>
```

# 四、状态先后的执行效果

## 4.1 resolve先、then先

```js
const promis = new Promise((resolve, reject) => {
  resolve("promis成功")
  reject("promis失败")
})

promis.then(res => {
  console.log("then回调", res)
}).catch(err => {
  console.log("cath回调", err)
})

//then回调 promis成功
```

> resolver 先决定了 promis 的状态，catch 的回调不会打印

## 4.2 resolve先、then后

```js
const promis = new Promise((resolve, reject) => {
  resolve("promis成功")
  reject("promis失败")
})

promis.catch((err) => {
  console.log("cath回调：", err)
}).then((res) => {
  console.log("then回调" ,res)
})

//then回调 promis成功
```

> resolve 已经确定为了 **兑现(fulfilled)** 状态，所以 catch 先监听也不可以改变 promes 的状态，状态还是 fulfilled 状态，所以打印 then 回调的结果

## 4.3 reject先、catch先

```js
const promis = new Promise((resolve, reject) => {
  reject("promis失败")
  resolve("promis成功")
})

promis.catch(err => {
  console.log("err回调", err)
}).then(res => {
  console.log("res回调", res)
})

//err回调 promis失败
//res回调 undefined
```

> reject 决定的 promise 状态，后面的 res 回调还是会打印，但是 resolve 回调的参数不会传递给 then 的，所以打印的 res 是 undefined


## 4.3 reject先、then先

```js
const promis = new Promise((resolve, reject) => {
  reject("promis失败")
  resolve("promis成功")
})

promis.then(res => {
  console.log("then回调", res)
}).catch(err => {
  console.log("cath回调", err)
})

//cath回调 promis失败
```

> reject 决定了状态，then 先监听不到，后面的 catch 监听就可以监听到，执行回调。

## 4.4 总结

只存在一种特殊的情况就是：

```js
const promis = new Promise((resolve, reject) => {
  reject("promis失败")
  resolve("promis成功")
})

promis.catch(err => {
  console.log("err回调", err)
}).then(res => {
  console.log("res回调", res)
})

//err回调 promis失败
//res回调 undefined
```

就是 reject先、catch先的情况下面，如果有 resovle 后面的回调，就会执行，但是不会把参数传递给回调函数


