# 一、Spread Attributes

我们实现一个一层层传递的案例:[Spread Attributes](https://zh-hans.react.dev/learn/passing-props-to-a-component#forwarding-props-with-the-jsx-spread-syntax)

有时候，传递 props 会变得非常重复：

```jsx
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

重复代码没有错（它可以更清晰）。但有时你可能会重视简洁。一些组件将它们所有的 props 转发给子组件，正如 `Profile` 转给 `Avatar` 那样。因为这些组件不直接使用他们本身的任何 props，所以使用更简洁的“展开”语法是有意义的：

```jsx
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

这会将 `Profile` 的所有 props 转发到 `Avatar`，而不列出每个名字。

如果还想传入下一层是不是就可以：

```jsx
function Avatar(props) {
  return (
    <div className="Avatar">
      <AvatarLast {...this.props} />
    </div>
  );
}
```

>[!note] 
>
>通过这样 `...this.props` 一直传递下去

# 二、Context应用场景

非父子组件数据的共享： 

- 在开发中，比较常见的数据传递方式是通过props属性自上而下（由父到子）进行传递。 
- 但是对于有一些场景：比如一些数据需要在多个组件中进行共享（地区偏好、UI主题、用户登录状态、用户信息等）。 
- 如果我们在顶层的App中定义这些信息，之后一层层传递下去，那么**对于一些中间层不需要数据的组件来说，是一种冗余的操作**。

但是，如果层级更多的话，一层层传递是非常麻烦，并且代码是非常冗余的： 

- React提供了一个API：**Context**； 
- Context 提供了一种在**组件之间共享此类值**的方式，而不必显式地通过组件树的逐层传递 props； 
- Context 设计目的是为了共享那些**对于一个组件树而言是“全局”的数据**，例如当前认证的用户、主题或首选语言；

## 2.1 Context相关API

**React.createContext** 

- 创建一个需要**共享的Context对象**： 
- 如果一个组件**订阅了Context**，那么这个组件会从**离自身最近**的那个匹配的 **Provider** 中读取到当前的context值； 
- defaultValue是组件在顶层查找过程中没有找到对应的Provider，那么就使用默认值

```jsx
const MyContext = React.createContext(defaultValue);
```

**Context.Provider** 

- 每个 Context 对象都会返回一个 Provider React 组件，它允许消费组件订阅 context 的变化： 
- Provider 接收一个 value 属性，传递给消费组件； 
- 一个 Provider 可以和多个消费组件有对应关系； 
- 多个 Provider 也可以嵌套使用，**里层的会覆盖外层的数据**；
- **当 Provider 的 value 值发生变化时，它内部的所有消费组件都会重新渲染**；

```jsx
<MyContext.Provider value={/*某个值*/}><MyContext.Provider/>
```

**Class.contextType**

- 挂载在 **类组件** 上的 contextType 属性会被重赋值为一个由React.createContext() 创建的 Context 对象： 
- 这能让你使用 this.context 来消费最近 Context 上的那个值； 
- 你可以在**任何生命周期**中访问到它，包括 render 函数中；

```jsx
类组件名称.contextType = MyContext
```

**Context.Consumer** 

- 这里，React 组件也可以订阅到 context 变更。这能让你在 **函数式组件** 中完成订阅 context。 
- 这里需要 **函数作为子元素**（function as child）这种做法； 
- 这个函数接收当前的 context 值，返回一个 React 节点；

```jsx
<MyContext.Consumer>
  {value => /*基于 context 值进行渲染*/}
</MyContext.Consumer>
```

## 2.2 Context演练

### 基本使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755155979000fjca7g.png)

类子组件里面也可以使用Context.Consumer来编写：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551562440003v3dtk.png)

### 默认值

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755156272000yaowwg.png)

> [!info] 
> 
> 子组件没有作为 UserContext.Provider 的 children 的时候，就可以使用默认值
> 


