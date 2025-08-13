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
