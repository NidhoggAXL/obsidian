# 一、为什么使用setState

开发中我们并不能直接通过修改state的值来让界面发生更新:

- 因为我们修改了state之后，希望React根据最新的State来重新渲染界面，但是这种方式的修改React并不知道数据发生了变化:
	
	- 不过，如果你修改了 state 里面的数据，数据本身是会发生变化的，只是不会通过 render 重新渲染
	
- React并没有实现类似于Vue2中的Obiect.defineProperty或者Vue3中的Proxy的方式来监听数据的变化;
	
- 我们**必须通过setState来告知React数据已经发生了变化**;
	
	- 就算调用 setState 里面**并没有数据进行更改**，**默认情况下也是会进行重新渲染的**
	- 到底要不要渲染，可以进行设置[[02 React组件生命周期#2.4 不常用生命周期函数|shouldComponentUpdate]]来判断

疑惑:在组件中并没有实现setState的方法，为什么可以调用呢?

- 原因很简单，setState方法是从Component中继承过来的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551616060004wkygk.png)

# 二、setState的用法

**用法一**：最基础的用法：

```jsx
this.setState({ key: value })
```

**用法二**：回调函数修改 state 里面的值

- 可以对 state、props 进行一些处理在进行修改，减少要对其改变而再次创建函数
- setState 第一个参数中，不过是什么拿到的都是修改前的 state 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755169552000ue5xaj.png)


**用法三**：传入第二个参数，要求是一个回调函数

- 可以进行逻辑的编写，以及修改完成的确定

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551698130001z1khf.png)

# 三、setState异步更新

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551692180005anwud.png)

setState的更新是异步的？

- 最终打印结果是Hello World； 
- 可见setState是异步的操作，我们并不能在执行完setState之后立马拿到最新的state的结果

为什么setState设计为异步呢？ 

- setState设计为异步其实之前在GitHub上也有很多的讨论； 
- React核心成员（Redux的作者）Dan Abramov也有对应的回复，有兴趣的同学可以参考一下； 
- https://github.com/facebook/react/issues/11527#issuecomment-360199710；

setState设计为异步，可以**显著的提升性能**； 

- 如果每次调用 setState都进行一次更新，那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的； 
- 最好的办法应该是获取到多个更新，之后**进行批量更新**；

**如果同步更新了state，但是还没有执行render函数，那么state和props不能保持同步**； 

- state和props不能保持一致性，会在开发中产生很多的问题；

# 四、获取异步的结果

**方式一**：setState的回调 

- setState接受两个参数：第二个参数是一个回调函数，这个回调函数会在更新后会执行； 
- 格式如下：setState(partialState, callback)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551700300005z3amo.png)

当然，我们也可以在[[02 React组件生命周期|生命周期]]函数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551700400009mzlli.png)

# 五、setState一定异步吗?(React18之前)

验证一：在setTimeout中的更新：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755173046000zubiqn.png)

验证二：原生DOM事件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755173053000yr1fxp.png)

其实分成两种情况：

- 在组件生命周期或React合成事件中，setState是异步；
- 在setTimeout或者原生dom事件中，setState是同步；

> [!tip] 这些同步代码的本质就是，本来该 **React 进行回调的函数**，通过编写**交给了浏览器来处理**

# 六、setState默认是异步的(React18之后)

在React18之后，默认所有的操作都被放到了批处理中（异步处理）。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755173243000fvnuf4.png)

如果希望代码可以同步会拿到，则需要执行特殊的flushSync操作：

```jsx
import flushSync form 'react-dom'
flushSnc(() => {
  this.setState({ counter: 1000 })
})
console.log(this.state.counter)//1000
```

> [!tip] 批处理自我理解：
> 和节流一样，在规定时间内执行一次，不过事件的多少都是在一定时间内统一执行






