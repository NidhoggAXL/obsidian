# 一、什么是组件化开发

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755066114000zpcj6h.png)

# 二、React的组件化
组件化是React的核心思想，也是我们后续课程的重点，前面我们封装的App本身就是一个组件:

- 组件化提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。
- 任何的应用都会被抽象成一颗组件树。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755066237000qitpwh.png)


**组件化思想的应用**:

- 有了组件化的思想，我们在之后的开发中就要充分的利用它,
- 尽可能的将页面拆分成一个个**小的、可复用**的组件。
- 这样让我们的代码更加方便组织和管理，并且扩展性也更强、

React的组件相对于Vue更加的灵活和多样，按照不同的方式可以分成很多类组件:

- **根据组件的定义方式**，可以分为:**函数组件(FunctionalComponent )** 和 **类组件(Class Component)**;
- 根据组件**内部是否有状态需要维护**，可以分成:**无状态组件(Stateless Component )** 和 **有状态组件(StatefulComponent);**
- 根据组件的**不同职责**，可以分成:**展示型组件(Presentational Component)** 和 **容器型组件(Container Component);**

这些概念有很多重叠，但是他们最主要是关注数据逻辑和UI展示的分离:

- 函数组件、无状态组件、展示型组件主要关注UI的展示;
- 类组件、有态组件、容器型组件主要关注数据逻辑;

当然还有很多组件的其他概念:比如异步组件、高阶组件等，

# 三、类组件

**类组件的定义有如下要求**： 

- **组件的名称是大写字符开头**（无论类组件还是函数组件） 
- 类组件需要继承自 React.Component 
- 类组件必须实现render函数

**使用class定义一个组件**： 

- **constructor是可选的**，我们通常在constructor中初始化一些数据；
- this.state中维护的就是我们组件内部的数据； 
- **render()** 方法是 class 组件中**唯一必须实现的方法**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755069262000rqiz6n.png)

# 四、render函数的返回值

当 render 被调用时，它会检查 this.props 和 this.state 的变化并返回以下类型之一：

- **React 元素**： 
	- 通常通过 JSX 创建。
	- 例如，`<div />`会被 React 渲染为 DOM 节点，`<MyComponent />`会被 React 渲染为自定义组件；
	- 无论是`<div />`还是`<MyComponent />`**均为 React 元素**。
- **数组或 fragments**：使得 render 方法可以返回多个元素。
- **Portals**：可以渲染子节点到不同的 DOM 子树中。
- **字符串或数值类型**：它们在 DOM 中会被渲染为文本节点 
- **布尔类型或null或undefined**：什么都不渲染。

# 五、函数组件

函数组件是**使用function来进行定义的函数**，只是这个函数会**返回和类组件中render函数返回一样的内容**。

函数组件有自己的特点（当然，后面会讲hooks，就不一样了）： 

- 没有生命周期，也**会被更新并挂载**，但是没有生命周期函数； 
- this关键字不能指向组件实例（因为没有组件实例）； 
- 没有内部状态（state）；

定义一个函数组件：

```jsx
export default function APP() {
  return (
    <div>hello world</div>
  )
}
```

