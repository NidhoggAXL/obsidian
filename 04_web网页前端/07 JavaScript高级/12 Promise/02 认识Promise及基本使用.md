在上面的解决方案中，我们确确实实可以解决请求函数得到结果之后，获取到对应的回调，但是它存在两个主要的问题： 

* 第一，我们需要**自己来设计回调函数、回调函数的名称、回调函数**的使用等； 
* 第二，对于**不同的人、不同的框架设计出来的方案是不同的**，那么我们必须耐心去看别人的源码或者文档，以便可以理解它 这个函数到底怎么用；

我们来看一下Promise的API是怎么样的： 

* Promise是一个类，可以翻译成 **承诺、许诺 、期约**； 
* 当我们需要的时候，**给予调用者一个承诺**：待会儿我会给你回调数据时，就可以创建一个Promise的对象； 
* 在通过new创建Promise对象时，我们需要**传入一个回调函数**，我们称之为**executor (执行人)**
	* 这个回调函数**会被立即执行**，并且**给传入另外两个回调函数resolve、reject**； 
	* 当我们**调用resolve(解决)回调函数时**，会执行Promise对象的**then方法传入的回调函数；** 
	* 当我们**调用reject(拒绝)回调函数时**，会执行Promise对象的**catch方法传入的回调函数；**


```js
<script>
  function exeCode(count) {
    const promis = new Promise((resolve, reject) => {
      setTimeout(() => {
        if (count > 0) {
          let total = 0
          for (let i = 0; i < count; i++ ) {
            total += i
          }
          resolve(total)
          } else {
            reject(`${count}有问题`)
          }
      }, 3000);
    })
    return promis
  }
  
  exeCode(10).then((total) => {
    console.log(`成功，total = ${total}`)
  })
  exeCode(-1).catch((count) => {
    console.log(count)
  })
</script>
```

