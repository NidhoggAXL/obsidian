# 一、认识JSX

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754962098000p73am3.png)

**这段element变量的声明右侧赋值的标签语法是什么呢？** 

- 它不是一段字符串（因为没有使用引号包裹）； 
- 它看起来是一段HTML元素，但是能在js中直接给一个变量赋值html吗？ 
- 其实是不可以的，如果将 **type="text/babel"** 去除掉，那么就会出现语法错误； 
- 它到底是什么呢？其实它是**一段jsx的语法**； 

**JSX是什么？** 

- JSX是一种JavaScript的语法扩展（extension），也在很多地方称之为JavaScript XML，因为看起就是一段XML语法； 
- 它用于描述UI界面，并且其完全可以和JavaScript融合在一起使用； 
- 它不同于Vue中的模块语法，你不需要专门学习模块语法中的一些指令（比如[[08 v-for渲染类型|v-for]]、[[06 Vue的条件渲染|v-if、v-else]]、[[03 v-bind绑定属性|v-bind]]）；


# 二、为什么Recat选择了JSX

React认为**渲染逻辑本质上与其他UI逻辑存在内在耦合**

- 比如UI需要绑定事件(button、a原生等等);
- 比如UI中需要展示数据状态;
- 比如在某些状态发生改变时，又需要改变U1;

他们之间是密不可分，所以React没有将标记分离到不同的文件中，而是**将它们组合到了一起，这个地方就是组件(Component)**

我们只需要知道，JSX其实是嵌入到JavaScript中的一种结构语法;

JSX的书写规范:

- JSX的顶层只能有一个根元素，所以我们很多时候会在外层包裹一个div元素(或者使用知识点的[[05 portals和fragment#二、fragment(片段)|Fragment]]);
- 为了方便阅读，**通常在isx的外层包裹一个小括号(html)**，这样可以方便阅读，并且jsx可以进行换行书写;
- JSX中的标签可以是单标签，也可以是双标签，

> [!tip]
> 
> 注意:如果是单标签，必须以/>结尾;




