# 一、redux融入react代码

目前redux在react中使用是最多的，所以我们需要将之前编写的redux代码，融入到react当中去。


核心代码主要是两个： 

- 在 [[02 React组件生命周期#2.3 常用生命周期|componentDidMount]] 中定义数据的变化，当数据发生变化时重新设置 counter; 
- 在发生点击事件时，调用store的dispatch来派发对应的action；

![[React使用redux计数器|100%]]

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755411550000vswzbd.png)

# 二、react-redux使用

开始之前需要强调一下，redux和react没有直接的关系，你完全可以在React, Angular, Ember, jQuery, or vanilla JavaScript中使用Redux。 

尽管这样说，redux依然是和React库结合的更好，因为他们是通过state函数来描述界面的状态，Redux可以发射状态的更新， 让他们作出相应。 

虽然我们之前已经实现了connect、Provider这些帮助我们完成连接redux、react的辅助工具，但是实际上redux官方帮助我们提供了 react-redux 的库，可以直接在项目中使用，并且**实现的逻辑会更加的严谨和高效。**

安装react-redux

```bash
yarn add react-redux
```

store里面的编写和上面编写相同（使用同一个Store）：

- 在全局App中引用store，并使用 Provider 提供，后面的 **store 本质是 value**。
- 需要使用的组件通过 connect 进行转换。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755415803000lb7ywc.png)


![gh|700](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755415928000wpwppt.png)

# 三、react-redux源码导读

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755416029000hgluw7.png)




