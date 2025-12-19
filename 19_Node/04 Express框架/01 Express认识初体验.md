# 一、认识Web框架

前面我们已经学习了使用http内置模块来搭建Web服务器，为什么还要使用框架？

 - 原生http在进行很多处理时，会较为复杂；
 - 有URL判断、Method判断、参数处理、逻辑代码处理等，都需要我们自己来处理和封装；
 - 并且所有的内容都放在一起，会非常的混乱；

目前在Node中比较流行的Web服务器框架是express、koa；

 - 我们先来学习express，后面再学习koa，并且对他们进行对比；

express早于koa出现，并且在Node社区中迅速流行起来：

 - 我们可以基于express快速、方便的开发自己的Web服务器；
 - 并且可以通过一些实用工具和中间件来扩展自己功能；

> [!tip]
> Express整个框架的核心就是中间件，理解了中间件其他一切都非常简单！

# 二、Express安装

express的使用过程有两种方式：

 - 方式一：通过express提供的脚手架，直接创建一个应用的骨架；
 - 方式二：从零搭建自己的express应用结构；

方式一：安装express-generator

 - 安装脚手架

```bash
npm install -g express-generator
```

 - 创建项目

```bash
express express-demo
```

- 安装依赖

```bash
npm install
```

 - 启动项目

```bash
node bin/win
```

方式二：从零搭建自己的express应用结构；

```bash
npm init -y
```

# 三、Express的基本过程

我们来创建第一个express项目：

 - 会发现，之后的开发过程中，可以方便的将请求进行分离：、
	 - node 中的 http 是统一进行请求的，需要通过 [[02 http模块#五、request对象|http模块中的request对象]] 中获取
 - 无论是不同的URL，还是get、post等请求方式；
 - 这样的方式非常方便我们已经进行维护、扩展；
 - 当然，这只是初体验，接下来我们来探索更多的用法；

```js
import express from 'express'

// 创建服务器
const app = express()

// /home 的get请求
app.get("/home", (req, res) => {
  res.send("get请求home数据")
})

// /login 的post请求
app.post("/login", (req, res) => {
  res.send("post请求login登录")
})

// 监听端口
app.listen(8000, () => {
  console.log("服务器启动了")
})

```


