# 一、架构上

express是完整和强大的，其中帮助我们内置了非常多好用的功能；

koa是简洁和自由的，它只包含最核心的功能，并不会对我们使用其他中间件进行任何的限制。

 - 甚至是在app中连最基本的get、post都没有给我们提供；
 - 我们需要通过自己或者路由来判断请求方式或者其他功能；

# 二、中间件

express和koa框架他们的核心其实都是中间件：

 - 但是他们的中间件事实上，它们的中间件的执行机制是不同的，特别是针对某个中间件中包含异步操作时；
 - 所以，接下来，我们再来研究一下express和koa中间件的执行顺序问题；

# 三、案例

我通过一个需求来演示所有的过程：
 - 假如有三个中间件会在一次请求中匹配到，并且按照顺序执行；
 - 我希望最终实现的方案是：
	 - 在middleware1中，在req.message中添加一个字符串 aaa；
	 - 在middleware2中，在req.message中添加一个 字符串 bbb；
	 - 在middleware3中，在req.message中添加一个 字符串 ccc；
	 - 当所有内容添加结束后，在middleware1中，通过res返回最终的结果；

## 3.1 Koa同步数据实现

```js
import koa from "koa";

const app = new koa();

// 第一个同步中间件
app.use((ctx, next) => {
  console.log("middleware1");
  ctx.msg = "aaa";
  next();
  ctx.body = ctx.msg
});

// 第二个同步中间件
app.use((ctx, next) => {
  console.log("middleware1");
  ctx.msg += "bbb";
  next();
});

// 第三个同步中间件
app.use((ctx, next) => {
  console.log("middleware1");
  ctx.msg += "ccc"
});

app.listen(3000, () => {
  console.log("服务器开启");
});

```

放回的结果是：`aaabbbccc`

为什么会是这样呢？通过下面代码执行的流程图来看看 ctx.msg 在整个流程中的数值，就知道啦，同时也可以知道 Koa 的next的操作：

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766319080000ysujbo.png)


```txt
服务器开启
middleware1
middleware2
middleware3
```

> [!tip] 
> 当中间件执行完成后，如果上一个中间件的 next() 后面还有要执行的程序，那么会执行完 next() 后面的程序，并再次返回上一个中间件执行相同的逻辑，直到第一个匹配的中间件 next 后面的程序。

## 3.2 Koa异步数据实现

在工作中，可能会在某一个中间中，执行其他的异步请求代码，例如：网络请求、SQL语句查询。

那就想来看看下面的代码：在第三个中间件中进行网络请求

```js
import axios from "axios";
import koa from "koa";

const app = new koa();

// 第一个同步中间件
app.use((ctx, next) => {
  console.log("middleware1");
  ctx.msg = "aaa";
  next();
  ctx.body = ctx.msg;
});

// 第二个同步中间件
app.use((ctx, next) => {
  console.log("middleware1");
  ctx.msg += "bbb";
  next();
});

// 第三个异步中间件
app.use(async (ctx, next) => {
  console.log("middleware1");
  // 执行异步网络请求
  const res = await axios.get("http://codercba.com:1888/airbnb/api/home/discount")
  console.log(res.data.title)//热门目的地
  ctx.msg += res.data.title;
});

app.listen(3000, () => {
  console.log("服务器开启");
});

```

返回的结果是：`aaabbb`

结果不应该是这样啊！按照上面的逻辑，应该是 `aaabbb热门目的地` 为什么会这样呢？

> [!tip]
> 
> 如果 next() 执行的下一个中间件是一个异步函数，那么next默认不会等到中间件的结果，就会执行下一步程序。
> 
> **要注意**：是执行了 第三个异步中间件，但是不会等到第三个异步中间件的结果，就会执行第二个中间件的 next() 后面的程序。


那么如果是想获取到正确的数据，需要如何做呢？

> [!node] 在 next 前面添加 await 等到下一个中间的结果再执行 next 后面的程序。

```js
import axios from "axios";
import koa from "koa";

const app = new koa();

// 第一个异步同步中间件
app.use(async (ctx, next) => {
  console.log("middleware1");
  ctx.msg = "aaa";
  await next();
  ctx.body = ctx.msg;
});

// 第二个异步同步中间件
app.use(async (ctx, next) => {
  console.log("middleware1");
  ctx.msg += "bbb";
  await next();
});

// 第三个同步中间件
app.use(async (ctx, next) => {
  console.log("middleware1");
  // 执行异步网络请求
  const res = await axios.get("http://codercba.com:1888/airbnb/api/home/discount")
  console.log(res.data.title)//热门目的地
  ctx.msg += res.data.title;
});

app.listen(3000, () => {
  console.log("服务器开启");
});

```

这样每一个 next 都会等到结果，这样就可以正确的获取到全部数据。

## 3.3 Express同步数据实现

```js
import express from 'express'

const app = express()

app.use((req, res, next) => {
  console.log("express middleware1")
  req.msg = "aaa"
  next()
  res.json(req.msg)
})

app.use((req, res, next) => {
  console.log("express middleware2")
  req.msg += 'bbb'
  next()
})

app.use((req, res, next) => {
  console.log("express middleware3")
  req.msg += "ccc"
})

app.listen(8000, () => {
  console.log("服务开启")
})
```

放回结果：`aaabbbccc`

流程图和 [[#3.1 Koa同步数据实现|Koa同步数据实现]] 相同。

## 3.4 Express异步数据实现

那么，如果和 Koa 一样使用异步数据实现，可以得到正确的结果吗？先看代码：

```js
import express from 'express'
import axios from 'axios'

const app = express()

app.use(async (req, res, next) => {
  console.log("express middleware1")
  req.msg = "aaa"
  await next()
  res.json(req.msg)
})

app.use(async (req, res, next) => {
  console.log("express middleware2")
  req.msg += 'bbb'
  await next()
})

app.use(async (req, res, next) => {
  // 执行异步网络请求
  const resData = await axios.get("http://codercba.com:1888/airbnb/api/home/discount")
  // console.log(res.data.title)//热门目的地
  req.msg += resData.data.title;
})

app.listen(8000, () => {
  console.log("服务开启")
})
```

返回的结果：`aaabbb`

会发现Koa同样的编写程序，但是没有得到正确的结果，这到底是为什么呢？

> [!tip] 这种的根本原因是？
> Koa 的 next() 返回结果是一个 Promise：
> ![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766322890000u1fswe.png)
> Express的 next() 返回的结果是 void：
> ![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766322935000yau01l.png)


# 四、总结

Koa 和 Express 的根本区别就是这里的 next() 返回的类型不同，一个 Promsie ，一个是 void，这样就导致：

- 同步数据的时候，两个框架对数据的处理是一样的
- 异步数据的时候，Koa 可以再任何一个中间件中进行数据的返回，而 <mark class="hltr-cyan">Express 框架的话就只能再最后一个执行完的中间件进行数据的放回。</mark>



