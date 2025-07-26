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
* 在之后**我们去调用reject时，已经不会有任何的响应了**（并不是这行代码不会执行，而是无法改变Promise状态）；


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

