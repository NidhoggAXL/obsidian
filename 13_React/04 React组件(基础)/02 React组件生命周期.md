# 一、认识生命周期

很多的事物都有从创建到销毁的整个过程，这个过程称之为是生命周期;

React组件也有自己的生命周期，了解组件的生命周期可以让我们**在最合适的地方完成自己想要的功能**;

生命周期和生命周期函数的关系:

**生命周期**是一个**抽象的概念**，在生命周期的整个过程，分成了很多个阶段;

- 比如装载阶段(Mount)组件第一次在DOM树中被渲染的过程;
- 比如更新过程(Update)，组件状态发生变化，重新更新渲染的过程;
- 比如卸载过程(Unmount)组件从DOM树中被移除的过程;

React内部为了告诉我们当前处于哪些阶段，会对我们组件内部实现的**某些函数进行回调**，这些函数就是**生命周期函数**:

- 比如实现componentDidMount函数:组件已经挂载到DOM上时，就会回调;
- 比如实现componentDidUpdate函数:组件已经发生了更新时，就会回调;
- 比如实现componentWilUnmount函数:组件即将被移除时，就会回调;
- 我们可以在这些回调函数中编写自己的逻辑代码，来完成自己的需求功能;

我们谈React生命周期时，**主要谈的类的生命周期**，因为函数式组件是没有生命周期函数的;(后面可以通过hooks来模拟一些生命周期的回调)

> [!tip] 我们是在对这些回调函数进行声明，但是进行回调的是 React ，并不是我们进行的调用。

# 二、生命周期解析

组件的生命周期，主要分为两个阶段：Render phase(渲染阶段)、Commit phase(提交阶段)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755074217000i6txrg.png)

## 2.1  Render Phase（渲染阶段）

[https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/render-phase.png](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/render-phase.png)

- **核心特性**：
    
    - **纯函数 & 无副作用**：  
        此阶段仅负责**计算组件的输出**（JSX 结构），不允许修改 DOM、发起网络请求或执行任何可能改变外部状态的操作。
        
    - **可被中断/重启**：  
        React 可能因高优先级任务（如用户交互）暂停当前渲染，稍后重新开始，确保页面响应流畅（Concurrent Mode 的核心机制）。
        
- **包含的生命周期方法**（类组件）：
    
    - `render()`
        
    - `shouldComponentUpdate()`
    
    - `getDerivedStateFromProps()`
        
- **函数组件行为**：  
    函数组件本身就是一个渲染函数，其执行过程属于 Render Phase。


## 2.2 Commit Phase（提交阶段）

[https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/commit-phase.png](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/commit-phase.png)

- **核心特性**：
    
    - **操作 DOM & 执行副作用**：  
        React 将 Render Phase 计算的变更**一次性提交到真实 DOM**，此时可安全操作 DOM、发起请求等。
        
    - **调度更新**：  
        可触发新的状态更新（如 `setState`），但会进入下一轮渲染流程（避免循环更新）。
        
    - **同步且不可中断**：  
        此阶段必须连续执行完成，确保 DOM 状态的一致性。
        
- **包含的生命周期方法**（类组件）：
    
    - `componentDidMount()`
        
    - `componentDidUpdate()`
        
    - `getSnapshotBeforeUpdate()`
        
- **函数组件等价操作**：  
    通过 `useEffect` 或 `useLayoutEffect` 执行副作用（`useLayoutEffect` 在 DOM 更新后同步执行，类似 `componentDidMount/Update`）。

**关键差异总结：**

| **特性**    | Render Phase        | Commit Phase   |
| --------- | ------------------- | -------------- |
| **主要任务**  | 计算 JSX 结构           | 更新 DOM & 执行副作用 |
| **是否纯函数** | ✅ 必须无副作用            | ❌ 可操作外部状态      |
| **可中断性**  | ✅ 可被 React 暂停/重启    | ❌ 同步执行不可中断     |
| **性能影响**  | 可优化（如 `React.memo`） | 避免耗时操作阻塞页面     |

> [!tip] 为什么这样设计？
> React 通过分离渲染和提交阶段实现：
>1. **并发渲染（Concurrent Mode）**：在 Render Phase 暂停低优先级渲染，优先处理用户交互。
> 2. **一致性**：确保 DOM 更新是原子操作，避免中间状态暴露给用户。
> 3. **性能**：将耗时的渲染计算（可中断）与必要的 DOM 操作（不可中断）解耦。

> [!caution] **违反规则的后果**：在 Render Phase 执行副作用（如修改 DOM）会导致 UI 不一致或崩溃，因为该阶段可能被重复执行多次。
## 2.3 常用生命周期

最基础、最常用的生命周期函数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755074098000fp4dnf.png)


**Constructor**：

- 如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。
- constructor中通常只做两件事情： 
- 通过给 this.state 赋值对象来初始化内部的state； 
- 为事件绑定实例（this）；

**componentDidMount**

- componentDidMount() 会在组件挂载后（插入 DOM 树中）立即调用。
- componentDidMount中通常进行哪里操作呢？ 
	- 依赖于DOM的操作可以在这里进行； 
	- 在此处发送网络请求就最好的地方；（官方建议） 
	- 可以在此处添加一些订阅（会在componentWillUnmount取消订阅）；


**componentDidUpdate** ：

- componentDidUpdate() 会在更新后会被立即调用，首次渲染不会执行此方法。 
- 当组件更新后，可以在此处对 DOM 进行操作； 
- 如果你对更新前后的 props 进行了比较，也可以选择在此处进行网络请求；（例如，当 props 未发生变化时，则不会执行网 络请求）。

**componentWillUnmount** 

- componentWillUnmount() 会在组件卸载及销毁之前直接调用。 
- 在此方法中执行必要的清理操作； 
- 例如，清除 timer，取消网络请求或清除在 componentDidMount() 中创建的订阅等；

## 2.4 不常用生命周期函数

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755074702000075uts.png)


除了上面介绍的生命周期函数之外，还有一些不常用 的生命周期函数：

- **getDerivedStateFromProps**：state 的值在任何 时候都依赖于 props时使用；该方法返回一个对象 来更新state； 
- **getSnapshotBeforeUpdate**：在React更新DOM 之前回调的一个函数，可以获取DOM更新前的一 些信息（比如说滚动位置）； 
	- 第一个参数：prevProps（获取更新前props数据）
	- 第二个参数：prevState（获取更新前的this.state数据）
	- 第三个参数：shnapshot（获取更新前的一些信息）
- **shouldComponentUpdate**：<mark class="hltr-orange">该生命周期函数很常用</mark>，但是我们等待讲性能优化时再来详细讲解； 
	
	-  `nextProps`：组件即将用来渲染的下一个 props。将 `nextProps` 与 [`this.props`](https://zh-hans.react.dev/reference/react/Component#props) 进行比较以确定发生了什么变化。
	
	- `nextState`：组件即将渲染的下一个 state。将 `nextState` 与 [`this.state`](https://zh-hans.react.dev/reference/react/Component#props) 进行比较以确定发生了什么变化。
	
	- `nextContext`：组件将要渲染的下一个 context。将 `nextContext` 与 [`this.context`](https://zh-hans.react.dev/reference/react/Component#context) 进行比较以确定发生了什么变化。仅当你指定了 [`static contextType`](https://zh-hans.react.dev/reference/react/Component#static-contexttype) 时才可用。
	
	- 返回的结果为true（默认值），则执行后面的 render ，重新渲染
	
	- 返回的结果为false，则不执行后面的 render ，不会重新渲染
	
	- 默认返回的是true，也就是只要state发生改变，就会调用render方法；


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755160716000qz8tka.png)


另外，React中还提供了一些过期的生命周期函数，这 些函数已经不推荐使用。 更详细的生命周期相关的内容，可以参考官网： https://zh-hans.reactjs.org/docs/reactcomponent.html


