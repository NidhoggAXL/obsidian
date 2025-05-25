# 一、axios请求方式
支持多种请求方式: 

* `axios(config)` 
* `axios.request(config)`
* `axios.get(url[, config])`
* `axios.delete(url[, config])` 
* `axios.head(url[, config])` 
* `axios.post(url[, data[, config]])` 
* `axios.put(url[, data[, config]])`
* `axios.patch(url[, data[, config]])` 


有时候, 我们可能需求同时发送两个请求

* 使用axios.all, 可以放入多个请求的数组. 
* `axios.all([])` 返回的结果是一个数组，使用 axios.spread 可将数组 `[res1,res2]` 展开为 res1, res2

# 二、常见的配置选项

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748164590000k2xsx5.png)

# 三、常见请求演练

> [!tip] 通过axios请求的数据会和原始数据不同
> 这是因为axios给我们默认添加了一些属性再给我们返回的，如果想拿到原始数据的话，只用把传给我们的数据 .data 就是原始数据啦。

```js
// 1.发送request请求
axios.request({
  url: "http://123.207.32.32:8000/home/multidata",
  method: "get"
}).then(res => {
  console.log("res:", res.data)
})

// 2.发送get请求
axios.get(`http://123.207.32.32:9001/lyric?id=500665346`).then(res => {
  console.log("res:", res.data.lrc)
})
axios.get("http://123.207.32.32:9001/lyric", {
  params: {
    id: 500665346
  }
}).then(res => {
  console.log("res:", res.data.lrc)
})


// 3.发送post请求
axios.post("http://123.207.32.32:1888/02_param/postjson", {
  name: "coderwhy",
  password: 123456
}).then(res => {
  console.log("res", res.data)
})

axios.post("http://123.207.32.32:1888/02_param/postjson", {
  data: {
    name: "coderwhy",
    password: 123456
  }
}).then(res => {
  console.log("res", res.data)
})
```

# 四、baseURL和all

```js
// 1.baseURL
const baseURL = "http://123.207.32.32:8000"

// 给axios实例配置公共的基础配置
axios.defaults.baseURL = baseURL
axios.defaults.timeout = 10000
axios.defaults.headers = {}

// 1.1.get: /home/multidata
axios.get("/home/multidata").then(res => {
  console.log("res:", res.data)
})

// 1.2.get: /home/data

// 2.axios发送多个请求
// Promise.all
axios.all([
  axios.get("/home/multidata"),
  //如果是填写绝对的地址，那么baseRUL就再本次请求失效
  axios.get("http://123.207.32.32:9001/lyric?id=500665346")
]).then(res => {
  console.log("res:", res)
})
```
