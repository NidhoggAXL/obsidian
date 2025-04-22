# 一、resolve方法
前面我们学习的then、catch、finally方法都属于**Promise的实例方法**，都是存放在Promise的prototypey原型上的。 

* 下面我们再来学习一下**Promise的类方法**。

有时候我们已经有一个现成的内容了，希望将其转成Promise来使用，这个时候我们可以使用 Promise.resolve 方法来完成。 

* Promise.resolve的用法相当于new Promise，并且执行resolve操作：

```js
Promise.resolve("axl")
//等价于
new Promise((resolve) => resolve("axl"))
```


resolve参数的形态： 

* 情况一：参数是一个普通的值或者对象 
* 情况二：参数本身是Promise 
* 情况三：参数是一个thenable


# 二、reject方法

reject方法类似于resolve方法，只是会将Promise对象的状态设置为reject状态。 

Promise.reject的用法相当于new Promise，只是会调用reject：

```js
Promise.reject("axl")
//等价于
new Promise((resolve, resolve) => reject("axl"))
```

Promise.reject传入的参数无论是什么形态，都会直接作为reject状态的参数传递到catch的。


# 三、all方法-重点

另外一个类方法是Promise.all： 

* 它的作用是**将多个Promise包裹在一起形成一个新的Promise**； 
* 新的Promise状态由包裹的**所有Promise共同决定**： 

当**所有的**Promise状态变成fulfilled状态时，新的Promise状态为fulfilled，并且会**将所有Promise的返回值组成一个数组**； 

```js
<script>
  const p1 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p1 is Promise")
    }, 2000);
  })    

  const p2 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p2 is Promise")
    }, 3000);
  })    

  const p3 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p3 is Promise")
    }, 5000);
  })
  
  Promise.all([p1, p2, p3]).then((res) => {
    console.log("res is :", res)
    //res is : (3) ['p1 is Promise', 'p2 is Promise', 'p3 is Promise']
  })
</script>
```

当**有一个**Promise状态为reject时，新的Promise状态为reject，并且会将**第一个reject的返回值作为参数**；

```js
<script>
  const p1 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p1 is Promise")
    }, 2000);
  })    

  const p2 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reject("p2 reject error")
    }, 3000);
  })    

  const p3 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p1 is Promise")
    }, 5000);
  })
  
  Promise.all([p1, p2, p3]).then((res) => {
    console.log("res is :", res)
  }).catch((err) => {
    console.log("err is:", err)
    //err is: p2 reject error
  })
</script>
```


# 四、allSettled方法-了解
all方法有一个缺陷：当有其中一个Promise变成reject状态时，新Promise就会立即变成对应的reject状态。 

* 那么对于resolved的，以及依然处于pending状态的Promise，我们是获取不到对应的结果的； 

在ES11（ES2020）中，添加了新的API Promise.allSettled： 

* 该方法会在**所有的Promise都有结果（settled）**，无论是fulfilled，还是rejected时，才会有最终的状态； 
* 并且这个Promise的**结果一定是fulfilled的**；

```js
<script>
  const p1 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p1 is Promise")
    }, 2000);
  })   
  
  const p2 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reject("p2 reject error")
    }, 3000);
  })    

  const p3 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p1 is Promise")
    }, 5000);
  })
  
  Promise.allSettled([p1, p2, p3]).then((res) => {
    console.log("allSettled :", res)
  })
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732630527000xd46kp.png)

allSettled的结果是一个数组，数组中存放着每一个Promise的结果，并且是对应一个对象的； 

* 这个对象中包含status状态，以及对应的value值；

# 五、race方法-了解
如果有一个Promise有了结果，我们就希望决定最终新Promise的状态，那么可以使用race方法： 

* race是竞技、竞赛的意思，表示多个Promise相互竞争，谁先有结果，那么就使用谁的结果；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732630661000imtdpe.png)

# 六、any方法

any方法是ES12中新增的方法，和race方法是类似的： 

* any方法会**等到一个fulfilled状态，才会决定新Promise的状态**； 


```js
<script>
  const p1 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reject("p1 reject error")
    }, 2000);
  })    
  
  const p2 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p2 is promise")
    }, 3000);
  })    
  
  const p3 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reslove("p3 is Promise")
    }, 5000);
  })
  
  Promise.any([p1, p2, p3]).then((res) => {
    console.log("allSettled :", res)
    //allSettled : p2 is promise
  }).catch((err) => {
    console.log("err")
  })
</script>
```


* 如果所有的Promise都是reject的，那么也会等到所有的Promise都变成rejected状态；

```js
<script>
  const p1 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reject("p1 reject error")
    }, 2000);
  })    
  
  const p2 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reject("p2 reject error")
    }, 3000);
  })    
  
  const p3 = new Promise((reslove, reject) => {
    setTimeout(() => {
      reject("p3 reject error")
    }, 5000);
  })
  
  Promise.any([p1, p2, p3]).then((res) => {
    console.log("allSettled :", res)
  }).catch((err) => {
    console.log("err is:",err)
    //err is: AggregateError: All promises were rejected
  })
</script>
```



