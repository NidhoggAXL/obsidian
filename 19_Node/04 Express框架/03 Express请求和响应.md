# 一、客户端发送请求的方式

客户端传递到服务器参数的方法常见的是5种：

 - 方式一：通过get请求中的URL的params；
 - 方式二：通过get请求中的URL的query；
 - 方式三：通过[[02 Express中间件#3.3 express的中间件|post请求中的body的json格式]]；
 - 方式四：通过[[02 Express中间件#4.2 express.urlencoded|post请求中的body的x-www-form-urlencoded格]]；
 - 方式五：通过[[02 Express中间件#解析form-data|post请求中的form-data格式]]；

# 二、传递参数params

请求地址:http://localhost:8000/login/1/2

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766234282000k5z2h8.png)


获取参数：

```js
import express from 'express'

// 开启服务器
const app = express()

// 中间件
app.use("/login/:id/:name", (req, res, next) => {
  console.log(req.params)//[Object: null prototype] { id: '1', name: '2' }
  res.end(`请求的id=>${req.params.id},name=>${req.params.name}`)
  //请求的id=>1,name=>2
})

// 监听启动
app.listen(8000)

```


# 三、传递参数query

请求地址:http://localhost:8000/login?username=axl&password=123

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766234747000o0h0cd.png)


获取参数：

```js
import express from 'express'

// 开启服务器
const app = express()

// 中间件
app.use("/login", (req, res, next) => {
  console.log(req.query)
  //[Object: null prototype] { username: 'axl', password: '123' }
  res.end("OK")
})

// 监听启动
app.listen(8000)

```

# 四、响应数据

## 4.1 end方法

**end方法**：类似于http中的response.end方法，用法是一致的


```js
import express from 'express'

// 开启服务器
const app = express()

// 中间件
app.use((req, res, next) => {
  // 响应数据
  res.send('hello world')
})

// 监听启动
app.listen(8000)

```

响应的结果：响应的类型是 `text/html;charset=utf-8`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766235499000psdbek.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17662355100007p3rem.png)

## 4.2 json方法

**json方法**：json方法中可以传入很多的类型：object、array、string、boolean、number、null等，它们会被转换成json格式返回；

```js
import express from 'express'

// 开启服务器
const app = express()

// 中间件
app.post("/login", (req, res, next) => {
  // 响应数据
  const data = {
    code: 0,
    list: [
      {
        name: "张三",
        age: 18
      },
      {
        name: "李四",
        age: 20
      }
    ]
  }
  res.json(data)
})

// 监听启动
app.listen(8000)

```

响应的结果：响应的类型是 `application/json;charset=utf-8`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176623562600079f0mh.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766235646000pdag8r.png)

## 4.3 status方法

**status方法**：

 - 用于设置状态码；
 - 注意：这里是一个函数，而不是属性赋值；

```js
import express from 'express'

// 开启服务器
const app = express()

// 中间件
app.post("/login", (req, res, next) => {
  // 响应数据
  res.status(205)
  res.end("OK")
})

// 监听启动
app.listen(8000)

```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17662358740001jamh8.png)

## 4.4 更多响应数据

更多响应的方式：https://www.expressjs.com.cn/4x/api.html#res

