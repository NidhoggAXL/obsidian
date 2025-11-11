# 一、Portals的使用

#渲染根节点之外/react

某些情况下，我们希望渲染的内容独立于父组件，甚至是独立于当前挂载到的DOM元素中（默认都是挂载到id为root的DOM 元素上的）。

**Portal(门户)** 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的优秀的方案： 

- **第一个参数**（child）是任何可渲染的 React 子元素，例如一个元素，字符串或 fragment； 
- **第二个参数**（container）是一个 DOM 元素；

```jsx
ReactDom.createPortal(child, container)
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755307658000a4t6qo.png)


通常来讲，当你从组件的 render 方法返回一个元素时，该元素将被挂载到 DOM 节点中离其最近的父节点： 

## 1.1 Modal组件案例

然而，有时候将子元素插入到 DOM 节点中的不同位置也是有好处的：

比如说，我们准备开发一个Modal组件，它可以将它的子组件渲染到屏幕的中间位置： 

- 步骤一：修改index.html添加新的节点 
- 步骤二：编写这个节点的样式 
- 步骤三：编写组件代码

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755307882000yo342v.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755307797000y4nb6p.png)

# 二、fragment(片段)

在之前的开发中，我们总是在一个组件中返回内容时包裹一个div元素：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175530841200035jeek.png)


我们又希望可以不渲染这样一个div应该如何操作呢？ 

- 使用Fragment 
- Fragment 允许你将子列表分组，而无需向 DOM 添加额外节点；

```jsx
//不使用fragment
return (
  <div>
    <h1>我是内容</h1>
  </div>
)

//使用fragment
return (
  <fragment>
    <h1>我是内容</h1>
  </fragment>
)
```

React还提供了Fragment的短语法：

- 它看起来像空标签 `<> </>`
- 但是，**如果我们需要在Fragment中添加key**，那么就不能使用短语法

```jsx
//错误编写
< key="id">
</>
```

