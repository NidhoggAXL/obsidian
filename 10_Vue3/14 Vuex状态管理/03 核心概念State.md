# 一、单一状态树

Vuex 使用单一状态树:

- 用一个对象就包含了全部的应用层级的状态，
- 采用的是 **SSOT**，Single Source of Truth，也可以翻译成**单一数据源;**

这也意味着，<mark class="hltr-cyan">每个应用将仅仅包含一个 store 实例</mark>;
- 单状态树和模块化并不冲突，后面我们会讲到module的概念;

单一状态树的优势:

- 如果你的状态信息是保存到多个Store对象中的，那么之后的管理和维护等等都会变得特别困难
- 所以Vuex也使用了单一状态树来管理**应用层级的全部状态**
- 单一状态树能够使用最直接的方式找到某个状态的片段;
- 而且在之后的维护和调试过程中，也可以非常方便的管理和维护;

# 二、组件获取状态

处理在 template 中使用插值语法获取状态，也可以在使用 [[01 computed计算属性使用|position API 的 computed]] 

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17478351740005sr5zx.png)

但是，如果有很多个状态都需要获取话，可以使用**mapState的辅助函数**：

* mapState的方式一：对象类型； 
* mapState的方式二：数组类型； 
* 也可以使用<mark class="hltr-cyan">展开运算符和来原有的computed混合在一起</mark>；
* <mark class="hltr-cyan">展开运算后得到的就是每一个字符串匹配数据的 computed 的函数，例如上面 computed 中的 count 函数</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747835671000fbqkpb.png)

# 三、在setup中使用

在setup中如果单个获取状态是非常简单的： 

* 通过useStore拿到store后去获取某个状态即可； 
* 但是如果需要使用 mapState 的功能呢？

## 3.1 自己封装Hook

默认情况下，Vuex并没有提供非常方便的使用mapState的方式，下面进行了一个函数的封装：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837054000ld2ah6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837299000zr2qan.png)

> [!abstract]
> 
> 主要 bind 绑定，为什么要使用 bind 来绑定 this 到 store 呢？这是因为在 setup 中是不可以使用 this 的，这个时候就需要我们改变 this ，这样就可以使用this。


解构出来的本质是一个函数，而这个函数是 computed 中的属性，会使用到的this

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837244000o6nnbm.png)

## 3.1 解构和toRef结合使用(推荐)

[[05 解构Destructuring}|解构]] 和 [[05 ref知识点补充|toRefs]] 联合使用

* toRefs 保证是响应式
* 解构中如果有和data重复的数据，则可以起别名

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837427000yuj9sc.png)


