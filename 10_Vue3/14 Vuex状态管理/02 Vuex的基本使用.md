# 一、Vuex的安装

使用vuex，首先第一步需要安装vuex

```bash
npm install vuex
```
# 二、创建store

每一个Vuex应用的核心就是store(仓库)： store本质上是一个容器，它包含着应用中大部分的状态(state)

> [!abstract]
> 
> 在程序员的中有默认规则，都把创建的store放到 store 文件里面的 index.js 中
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747832334000b25n5g.png)


**Vuex和单纯的全局对象有什么区别呢？**

* 第一：Vuex的状态<mark class="hltr-cyan">存储是响应式</mark>的 
	* 当Vue组件从store中读取状态的时候，若store中的状态发生变化，那么相应的组件也会被更新； 
* 第二：你不能直接改变store中的状态 
	* 改变store中的状态的<mark class="hltr-cyan">唯一途径就显示提交mutation(转变)</mark>； 
	* 这样使得可以方便的跟踪每一个状态的变化，从而能够通过一些工具更好的管理应用的状态；

**使用步骤：** 

* 创建Store对象； 
	![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174783394000026878p.png)
* 在app中通过插件安装；
	![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747832358000p5omkn.png)

# 三、组件中使用store

在组件中使用store，我们按照如下的方式： 

在模板中使用； 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17478324630008hwmlt.png)

在options api中使用，比如computed； 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747833598000szj7h9.png)

在setup中使用；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747833651000r0k21a.png)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747833830000v5a43n.png)


如果是要修改 counter 的值的话：监听按钮，commit（提交）需要使用的mutations（转变）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747834120000wffc79.png)


