# 一、React中的插槽
在开发中，我们抽取了一个组件，但是为了让这个组件具备更强的通用性，我们不能将组件中的内容限制为固定的div、span等等 这些元素。 

我们应该让使用者可以决定某一块区域到底存放什么内容。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175513368300063aq0q.png)

这种需求在Vue当中有一个固定的做法是通过slot来完成的，React呢？

React对于这种需要插槽的情况非常灵活，有两种方案可以实现： 

- 组件的children子元素； 
- props属性传递React元素

# 二、children实现插槽

每个组件都可以获取到 props.children：它包含组件的开始标签和结束标签之间的内容。

如果是多个 ReactElement 元素，children 就是一个 数组。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755133611000ca6zua.png)

如果只有一个 ReactElement，那么 children 就是一个 对象：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755133930000y3lg75.png)


# 三、props实现插槽

通过children实现的方案虽然可行，但是有一个弊端：**通过索引值获取传入的元素很容易出错，不能精准的获取传入的原生；** 

- 有可能是一个数组或者元素，如果是数据必须确定索引的正确

另外一个种方案就是使用 props 实现：通过具体的属性名，可以让我们在传入和获取时更加的精准；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551344970006qo2a2.png)

# 四、作用域插槽

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755136454000c2v3ck.png)





