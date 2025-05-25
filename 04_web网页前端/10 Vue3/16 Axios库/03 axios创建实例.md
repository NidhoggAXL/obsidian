为什么要创建axios的实例呢? 

* 当我们从axios模块中导入对象时, 使用的实例是**默认的实例**；
* 当给该实例设置一些默认配置时, 这些配置就被固定下来了.
* 但是后续开发中, 某些配置可能会不太一样；
* 比如**某些请求需要使用特定的baseURL或者timeout**等.
* 这个时候, 我们就可以**创建新的实例,** 并且**传入属于该实例的配置信息.**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17481658860008yka8b.png)


```js
// axios默认库提供给我们的实例对象
axios.get("http://123.207.32.32:9001/lyric?id=500665346")

// 创建其他的实例发送网络请求
const instance1 = axios.create({
  baseURL: "http://123.207.32.32:9001",
  timeout: 6000,
  headers: {}
})

instance1.get("/lyric", {
  params: {
    id: 500665346
  }
}).then(res => {
  console.log("res:", res.data)
})

const instance2 = axios.create({
  baseURL: "http://123.207.32.32:8000",
  timeout: 10000,
  headers: {}
})
```

