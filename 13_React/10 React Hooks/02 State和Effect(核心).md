# 一、认识useState

State Hook的API就是 useState，我们在前面已经进行了学习： 

- useState会帮助我们定义一个 state变量，useState 是一种新方法，它与 class 里面的 this.state 提供的功能完全相同。 
- 一般来说，在函数退出后变量就会”消失”，而 state 中的变量会被 React 保留。
- useState接受唯一一个参数，在<mark class="hltr-orange">第一次组件被调用时使用来作为初始化值</mark>。（如果没有传递参数，那么初始化值为undefined）。 
- useState的返回值是一个数组，我们可以通过[[05 解构Destructuring#1.1 数组解构|数组的解构]]，来完成赋值会非常方便。
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring

FAQ：为什么叫 useState 而不叫 createState? 

- “create” 可能不是很准确，因为 state 只在组件首次渲染的时候被创建。 
- **在下一次重新渲染时，useState 返回给我们当前的 state**。 
- 如果每次都创建新的变量，它就不是 “state”了。
- 这也是 Hook 的名字总是以 use 开头的一个原因。

## 1.1 useState常见错误

<mark class="hltr-orange">useState 在第一次渲染的时候，初始化值就是已经确定的：</mark>

比如第一次渲染的时候如下面伪代码：

```jsx
const initCounter = ""
const [counter, setCounter] = useState(initCounter)
```

因为一些原因，不是通过 setCount 改变的 counter 的值，比如网络请求改变了 initCounter 的值，这个时候进行第二次渲染:

```jsx
const initCounter = 'axl'
const [counter, setCounter] = useState(initCounter)
```

> [!warning] 这个时候的 counter 还是 空字符串， 不会因为 initCounter 的改变而改变。

如果遇到这种情况，那么就在 initCounter 改变为不是 空字符 的时候，不要进行渲染(本质是执行 useState)

比如：第一次渲染 Home 组件的时候 initCounter 由外部传入，但是外部组件的内容需要网络请求才可以得到，在第一次渲染的时候 initCounter 就是为空字符串

```jsx
{
  Object.keys(outData).length && <Home initCounter={outData.initCounter} />
}
```

# 二、认识Effect Hook

目前我们已经通过hook在函数式组件中定义state，那么类似于生命周期这些呢？ 

- Effect Hook 可以让你来完成一些类似于class中[[02 React组件生命周期|生命周期]]的功能； 
- 事实上，类似于**网络请求、手动更新DOM、一些事件的监听**，都是React更新DOM的一些**副作用（Side Effects**）； 
- 所以对于完成这些功能的Hook被称之为 **Effect Hook**； 

**假如我们现在有一个需求**：页面的title总是显示counter的数字，使用Hook实现：

```jsx
import React, { memo, useEffect, useState } from 'react'

const App = memo(() => {
  const [count, setCount] = useState(200)

  useEffect(() => {
    document.title = count
  })

  return (
    <div>
      <h2>App</h2>
      <button onClick={e => setCount(count+1)}>+1</button>
    </div>
  )
})

export default App
```

useEffect的解析： 

- 通过useEffect的Hook，可以告诉React需要在渲染后执行某些操作； 
- useEffect要求我们传入一个回调函数，在**React执行完更新DOM操作之后**，就会回调这个函数； 
- 默认情况下，<mark class="hltr-orange">无论是第一次渲染之后，还是每次更新之后</mark>，都会执行这 **回调函数**；

# 三、需要清除Effect

在class组件的编写过程中，某些副作用的代码，我们需要在[[02 React组件生命周期#2.3 常用生命周期|componentWillUnmount]]中进行清除： 

- 比如我们之前的[[06 自定义事件总线|事件总线]]或Redux中手动调用[[02 Redux的使用#三、Redux结构划分|subscribe]]； 
- 都需要在componentWillUnmount有对应的取消订阅； 
- Effect Hook通过什么方式来模拟componentWillUnmount呢？

useEffect传入的**回调函数A**本身可以有一个返回值，这个返回值是另外一个**回调函数B**：

```ts
type EffectCallback = () => (void | (() => void | undefined));
```

为什么要在 effect 中返回一个函数？ 

- 这是 effect 可选的清除机制。**每个 effect 都可以返回一个清除函数**； 
- 如此可以将**添加和移除订阅的逻辑放在一起**； 
- 它们都属于 effect 的一部分； 

React 何时清除 effect？ 

- React 会在组件**更新和卸载**的时候执行清除操作； 
- 正如之前学到的，effect 在每次渲染的时候都会执行；

```jsx
import React, { memo, useEffect, useState } from 'react'

const App = memo(() => {
  const [count, setCount] = useState(200)

  useEffect(() => {
    console.log("一些副作用代码的监听")
    return () => {
      console.log("取消副作用代码的监听")
    }
  })

  return (
    <div>
      <h2>App</h2>
      <button onClick={e => setCount(count+1)}>+1</button>
    </div>
  )
})

export default App
```

如果点击按钮让函数组件重新渲染执行后的打印结果如下：

```text
一些副作用代码的监听
取消副作用代码的监听
一些副作用代码的监听
```

# 四、使用多个Effect

使用Hook的其中一个目的就是解决class中生命周期经常将很多的逻辑放在一起的问题： 

- 比如**网络请求、事件监听、手动修改DOM**，这些往往都会放在[[02 React组件生命周期#2.3 常用生命周期|componentDidMount]]中； 

使用Effect Hook，我们可以将它们分离到不同的useEffect中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17557612390006vxnlx.png)

> [!tip] 使用：
> **Hook 允许我们按照代码的用途分离它们**， 而不是像生命周期函数那样： 
> React 将按照 **effect 声明的顺序依次调用**组件中的每一个 effect；

# 五、Effect性能优化

默认情况下，**useEffect的回调函数会在每次渲染时都重新执行**，但是这会导致两个问题： 

- 某些代码我们只是希望执行一次即可，类似于 **componentDidMount** 和 **componentWillUnmount** 中完成的事情；（比如网络请求、订阅和取消订阅）； 
- 另外，多次执行也会**导致一定的性能问题**；

我们如何决定useEffect在什么时候应该执行和什么时候不应该执行呢？ 

- useEffect实际上有两个参数： 
- **参数一**：执行的回调函数； 
- **参数二**：该useEffect在哪些**state发生变化**时，**才重新执行**；（**受谁的影响**） 

**案例练习**：  受count影响的Effect； 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755761768000wtj1zw.png)


但是，如果一个函数我们不希望依赖任何的内容时，也可以传入一个**空的数组`[]`**： 

- 那么这里的两个回调函数分别对应的就是componentDidMount和componentWillUnmount生命周期函数了；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175576186000015j1ps.png)



