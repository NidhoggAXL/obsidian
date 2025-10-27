# 一、认识和定义State

state 是 store 的核心部分，因为store是用来帮助我们管理状态的。 

* 在 Pinia 中，状态被定义为返回初始状态的函数；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159506000ip73is.png)

# 二、操作State

## 2.1 读取和写入

**读取和写入 state**：  默认情况下，您可以通过 store 实例访问状态来直接读取和写入状态；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159556000bsk5ko.png)

## 2.2 $reset重置

**重置 State**： 你可以通过调用 store 上的 <mark class="hltr-cyan">$reset() 方法将状态重置到其初始值</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159571000yyccs2.png)

## 2.3 $patch多修改

**改变State：** 

* 除了直接用 store.counter++ 修改 store，你还可以调用 $patch 方法； 
* 它允许您使用部分“state”对象<mark class="hltr-cyan">同时应用多个更改</mark>；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159608000n60o9i.png)

## 2.4 $state替换

**替换State**：

* 可以通过将其 $state 属性设置为新对象来替换 Store 的整个状态：
* 但是这里的替换更像是一种合并，替换后的对象和原对象地址相同
* 也可以进行重置State

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748159700000dhcti8.png)

