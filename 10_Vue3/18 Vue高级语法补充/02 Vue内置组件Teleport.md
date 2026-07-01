# 一、认识Telepor(传送)

#渲染根节点之外/vue

在组件化开发中，我们封装一个组件A，在另外一个组件B中使用:

- 那么组件A中template的元素，会被挂载到组件B中template的某个位置;- 最终我们的应用程序会形成一颗DOM树结构

但是某些情况下，我们希望组件不是挂载在这个组件树上的，可能是移动到Vue app之外的其他位置

- 比如移动到body元素上，或者我们有其他的 `div#app` 之外的元素上;
- 这个时候我们就可以通过teleport来完成

Teleport是什么呢?

- 它是一个Vue提供的内置组件，类似于react的[[05 portals和fragment#一、Portals的使用|Portals]];
- teleport翻译过来是心灵传输、远距离运输的意思，

它有两个属性:
>to:指定将其中的内容移动到的目标元素，可以使用选择器，
> disabled:是否禁用 teleport 的功能;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753404658000ehgh5u.png)

# 二、Teleport效果

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534046940004bmee7.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753404699000zvk7rk.png)

# 三、和组件结合使用

当然，teleport也可以和组件结合一起来使用： 可以在 teleport 中使用组件，并且也可以给他传入一些数据；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753404828000m8vm0l.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534048320003j8n1g.png)

# 四、多个teleport

如果我们将**多个teleport应用**到同一个目标上（to的值相同），那么这些目标会进行**合并**：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534048760003au21y.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753404880000jol0pk.png)

