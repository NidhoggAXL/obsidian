
# 一、Promise面试题
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732947165000h3m9al.png)

![[Promise面试题一]]


# 二、Promise async await 面 试 题

## 2.1 await 前后代码的执行顺序
先查看下面这段代码的结果：

```js
<script>
  function requesData() {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        console.log("setTimeout")
        resolve("resolve")
      }, 2000);
    })
  }
  
  async function getData() {
    console.log("getData")
    const res = await requesData()
    console.log("res:", res)
    console.log("then1")
  }
  
  getData()
</script>
```

打印结果为：

```
script start
getData
script end
setTimeout
res: resolve
then1
```

> [!tip] 分析
> 当我们在运行到异步函数里面的关键字 await 的时候，会等 requesData() 的返回值 Promise 运行 resolve 的时候才会运行后面的代码。
> **重点：await 不执行后面的代码，是异步函数里面的代码。异步函数代码外的代码是会执行的。**

> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732951793000rhfhn5.png)
> 相当于 await 后面的 Promise 变为 resolve ，会进行 then 回调。
> ```js
> .then((res) => {
> console.log("res:", res)
> console.log("then1")
> })
> ```

## 2.2 Promise async await 面 试 题二
![[Promise面试题二.png]]

![[Promise面试题二]]

\

# 三、Promise setTimeout时间不为0

## 3.1 第一个题目

![[Promise面试题三.png]]

![[Promise面试题三]]



## 3.2 第二个题目
![[Promise面试题四.png]]


![[Promise面试题四]]




