# 一、Options API的弊端

在Vue2中，我们编写组件的方式是Options API

- Options APl的一大特点就是在**对应的属性中编写对应的功能模块**
- 比如data定义数据、methods中定义方法、computed中定义计算属性、watch中监听属性改变，也包括生命周期钩子

**但是这种代码有一个很大的弊端:**

- 当我们实现某一个功能时，这个**功能对应的代码逻辑会被拆分到各个属性中;**
- 当我们组件变得更大、更复杂时，逻辑关注点的列表就会增长，那么同一个功能的逻辑就会被拆分的很分散
- 尤其对于那些一开始没有编写这些组件的人来说，这个组件的代码是难以阅读和理解的(阅读组件的其他人)

下面看一个非常大的组件，其中的逻辑功能按照颜色进行了划分:

- 这种碎片化的代码使用理解和维护这个复杂的组件变得异常困难，并且隐藏了潜在的逻辑问题
- 并且当**处理单个逻辑关注点时，需要不断的跳到相应的代码块中;**

# 二、大组件的逻辑分散

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746884610000zjv6mu.png)


如果我们能将同一个<mark class="hltr-orange">逻辑关注点相关的代码收集在一起</mark>会更好。这就是Composition(组成) API想要做的事情，以及可以帮助我们完成的事情。 也有人把Vue Composition API简称为VCA。

# 三、认识composition API

那么既然知道Composition API想要帮助我们做什么事情，接下来看一到底是怎么做呢?

- 为了开始使用Composition AP!，我们需要有一个可以实际使用它(编写代码)的地方
- 在Vue组件中，这个位置就是 **setup函数**

setup其实就是组件的另外一个选项:

- 只不过这个选项**强大到可以用它来替代之前所编写的大部分其他选项生命周期**等等;
- 比如methods、computed、watch、 data、生命周期等等

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746884724000oznt8g.png)


