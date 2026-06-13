Nuxt3 提供了编写后端服务接口的功能，编写服务接口可以在server/api目录下编写

比如：编写一个 /api/homeinfo 接口

1. 在server/api目录下新建 homeinfo.ts
2. 接在在该文件中使用 **defineEventHandler** 函数来定义接口（支持 async）
3. 然后就可以用useFetch函数轻松调用： /api/homeinfo 接口了

```ts
export default defineEventHandler(async (event) => {
  // 从事件对象中解构出请求(req)和响应(res)对象 这些对象通常包含HTTP请求和响应的相关信息和方法
  const { req, res } = event.node

  // 一些req和res的使用
  // 下面打印只会在服务器打印，客户端看不到
  console.log(req.url)
  console.log(req.method)
  console.log(res.statusCode)

  // 全局的一些方法
  // 下面打印会在服务器和客户端都打印
  console.log(getQuery(event))
  console.log(getHeaders(event))
  console.log(await readBody(event))
  console.log(await readRawBody(event))

  // 返回数据
  return {
    code: 200,
    data: {
      title: '首页',
      content: '首页内容'
    }
  }
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774185656000v96q7s.png)


