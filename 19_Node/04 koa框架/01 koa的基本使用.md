# 一、认识koa

Koa官方的介绍：

 - koa：next generation web framework for node.js；
 - koa：node.js的下一代web框架；

事实上，koa是express同一个团队开发的一个新的Web框架：

 - 目前团队的**核心开发者TJ的主要精力也在维护Koa**，express已经交给团队维护了；
 - Koa旨在为Web应用程序和API提供**更小、更丰富和更强大的能力**；
 - 相对于express具有更强的异步处理能力；
 - Koa的核心代码只有**1600+行**，是一个**更加轻量级的框架**；
 - 我们可以根据**需要安装和使用中间件**；

# 二、koa初体验

来体验一下koa的Web服务器，创建一个接口：koa也是通过注册中间件来完成请求操作的；

koa注册的中间件提供了两个参数：

 - ctx：上下文（Context）对象；
	 - **koa并没有像express一样，将req和res分开，而是将它们作为ctx的属性**；
	 - ctx代表一次请求的上下文对象；
	 - ctx.request：获取请求对象；
	 - ctx.response：获取响应对象；
 - next：本质上是一个dispatch，类似于之前的next；
	  - 后续学习Koa的源码，来看一下它是一个怎么样的函数；


```js
import koa from 'koa'

// 创建服务器
const app = new koa()

// 开启服务器
app.listen(3000, () => {
  console.log('服务器启动成功')
})
```

如果没有返回数据，koa会默认返回一个 Not Fount，而express则会把请求挂起：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17663037600003779pq.png)

那么如何返回数据呢？通过 ctx.res 或者 ctx.response

> [!tip] res、req和response、request的区别？
>  - res、req 是Node封装的请求对象。
>  - response、request 是Koa封装的请求对象。


```js
import koa from 'koa'

// 创建服务器
const app = new koa()

// 中间件
// ctx是context上下文缩写
app.use((ctx, next) => {
  // node方式的放回数据
  // ctx.res.end("匹配到中间件")

  // Koa方式的返回数据
  ctx.response.body = "匹配到的中间件"
})

// 开启服务器
app.listen(3000, () => {
  console.log('服务器启动成功')
})
```

# 三、Koa中间件

koa通过创建的app对象，注册中间件只能通过use方法：

 - Koa并没有提供methods的方式来注册中间件；
 - 也没有提供path中间件来匹配路径；

但是真实开发中我们如何将路径和method分离呢？

 - 方式一：根据request自己来判断；
 - 方式二：使用第三方路由中间件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766304789000g8ozp8.png)

> [!tip]
> ctx.request 和 ctx.response 里面的大多数数据，都可以直接通过 ctx 直接来获取，比如：
> `ctx.resquest.path === ctx.path`

# 四、Koa路由

koa官方并没有给我们提供路由的库，我们可以选择第三方库：@koa-router

```bash
npm install @koa/router
```

> [!tip]
> 其实还有一个koa的路由库 koa-router ，但是 koa-router 好久没有维护了，所以使用官方维护的库 @koa/router

先封装一个 user.router.js 的文件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766305871000gugrhs.png)

在app中将router.routes()注册为中间件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766305903000urh2lr.png)

> [!tip] 注意：allowedMethods用于判断某一个method是否支持：
> 
>  - 如果我们请求 get，那么是正常的请求，因为我们有实现get；
>  - 如果我们请求 put、delete、patch，那么就自动报错：
> 	 - Method Not Allowed，状态码：405；
>  - 如果我们请求 link、copy、lock，那么就自动报错
> 	 - Not Implemented，状态码：501；


