# 一、认识纯函数

![[02 纯函数的理解和应用]]

# 二、认识redux

JavaScript开发的应用程序，已经变得越来越复杂了： 

- JavaScript需要管理的状态越来越多，越来越复杂； 
- 这些状态包括服务器返回的数据、缓存数据、用户操作产生的数据等等，也包括一些UI的状态，比如某些元素是否被选中，是否显示 加载动效，当前分页；

管理不断变化的state是非常困难的： 

- 状态之间相互会存在依赖，一个状态的变化会引起另一个状态的变化，View页面也有可能会引起状态的变化； 
- 当应用程序复杂时，state在什么时候，因为什么原因而发生了变化，发生了怎么样的变化，会变得非常难以控制和追踪；

**React是在视图层帮助我们解决了DOM的渲染过程，但是State依然是留给我们自己来管理**： 

- 无论是组件定义自己的state，还是组件之间的通信通过props进行传递；也包括通过Context进行数据之间的共享； 
- React主要负责帮助我们管理视图，state如何维护最终还是我们自己来决定； 

Redux就是一个帮助我们管理State的容器：Redux是JavaScript的状态容器，提供了**可预测的状态管理**；

Redux除了和React一起使用之外，它也可以和其他界面库一起来使用（比如Vue），并且它非常小（包括依赖在内，只有2kb）

# 三、Redux的核心理念-Store

Redux的核心理念非常简单。 

比如我们有一个朋友列表需要管理： 

- 如果我们没有定义统一的规范来操作这段数据，那么整个数据的变化就是无法跟踪的；
- 比如页面的某处通过`products.push`的方式增加了一条数据； 
- 比如另一个页面通过`products[0].age = 25`修改了一条数据； 

整个应用程序错综复杂，当出现bug时，很难跟踪到底哪里发生的变化；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755388647000w6fvew.png)

# 四、Redux的核心概念-action

Redux要求我们**通过action来更新数据**： 

- 所有数据的变化，必须通过派发（dispatch）action来更新； 
- action是一个**普通的JavaScript对象**，用来描述这次更新的**type和content**； 

比如下面就是几个更新friends的action： 

- 强制使用action的好处是可以清晰的知道数据到底发生了什么样的变化，**所有的数据变化都是可跟追、可预测的**； 
- 当然，目前我们的action是固定的对象； 
- 真实应用中，我们会通过函数来定义，返回一个action；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755388755000wc97kn.png)

# 五、Redux的核心理念-reducer

但是如何将state和action联系在一起呢？答案就是reducer 

- reducer是一个**纯函数**； 
- reducer做的事情就是将传入的state和action结合起来生成一个新的state；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755388829000gk7w0i.png)

# 六、Redux的三大原则

**单一数据源**：

- 整个应用程序的**state被存储在一颗object tree中**，并且这个object tree**只存储在一个 store 中**： 
- Redux并没有强制让我们不能创建多个Store，但是那样做并不利于数据的维护； 
- 单一的数据源可以让整个应用程序的state变得方便维护、追踪、修改； 

**State是只读的** 

- **唯一修改State的方法一定是触发action**，不要试图在其他地方通过任何的方式来修改State： 
- 这样就确保了View或网络请求都不能直接修改state，它们只能通过action来描述自己想要如何修改state； 
- 这样可以保证所有的修改都被集中化处理，并且按照严格的顺序来执行，所以不需要担心race condition（竟态）的问题； 

**使用纯函数来执行修改** 

- 通过reducer将 旧state和 actions联系在一起，并且**返回一个新的State**： 
- 随着应用程序的复杂度增加，我们**可以将reducer拆分成多个小的reducers，分别操作不同state tree的一部分**； 
- 但是所有的reducer都应该是纯函数，不能产生任何的副作用；

