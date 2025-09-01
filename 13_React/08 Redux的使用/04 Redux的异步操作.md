# 一、组件中异步操作

在之前简单的案例中，redux中保存的counter是一个本地定义的数据 

- 我们可以直接通过**同步**的操作来dispatch action，state就会被立即更新。 
- 但是真实开发中，redux中保存的很多数据可能**来自服务器**，我们需要进行**异步的请求**，再**将数据保存到redux中**。

在之前学习网络请求的时候我们讲过，网络请求可以在class组件的componentDidMount中发送，所以我们可以有这样的结构：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755422722000yb78gv.png)

我现在完成如下案例操作：  在Home组件中请求categories的数据，并把数据保存到store中，并从store中获取数据；


# 二、redux中异步操作

上面的代码有一个缺陷： 

- 我们必须将网络请求的异步代码放到组件的生命周期中来完成； 
- 事实上，网络请求到的数据也属于我们状态管理的一部分，更好的一种方式应该是将其也交给redux来管理；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175542031300004cfsp.png)

但是在redux中如何可以进行异步的操作呢？ 

- 答案就是**使用中间件（Middleware）**； 
- 学习过Express或Koa框架的童鞋对中间件的概念一定不陌生； 
- 在这类框架中，Middleware可以帮助我们在请求和响应之间嵌入一些操作的代码，比如cookie解析、日志记录、文件压缩等操作；

# 三、理解中间件

redux也引入了中间件（Middleware）的概念： 

- 这个中间件的目的是在dispatch的action和最终达到的reducer之间，扩展一些自己的代码； 
- 比如日志记录、调用异步接口、添加代码调试功能等等；

我们现在要做的事情就是发送异步的网络请求，所以我们可以添加对应的中间件： 

- 这里官网推荐的、包括演示的网络请求的中间件是使用 redux-thunk；


redux-thunk是如何做到让我们可以发送异步的请求呢？ 

- 默认情况下的dispatch(action)，**action需要是一个JavaScript的对象**；
- redux-thunk可以让**dispatch(action函数)**，**action可以是一个函数**； 
- 该函数会被调用，并且会传给这个函数一个**dispatch函数和getState函数**； 
	- dispatch函数用于我们之后再次派发action； 
	- getState函数考虑到我们之后的一些操作需要依赖原来的状态，用于让我们可以获取之前的一些状态；

# 四、如何使用redux-thunk

1. 安装redux-thunk 

```bash
npm install redux-thunk
```

2. 在创建store时传入应用了middleware的enhance函数 
	- 通过applyMiddleware来结合多个Middleware(中间件), 返回一个enhancer； 
	- 将enhancer作为第二个参数传入到createStore中；

```js
import { applyMiddleware, createStore } from "redux";
import reducer from './reducer'
import { thunk } from 'redux-thunk';  // 使用命名导入

const store = createStore(reducer, applyMiddleware(thunk))

export default store;
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755501258000xxbbnj.png)


3. 定义返回一个函数的action： 
	- 注意：这里不是返回一个对象了，而是一个函数； 
	- 该函数在dispatch之后会被执行；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755501229000pm1g68.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755501150000a8cxu5.png)



