# 一、新的ECMA代码执行描述
在执行学习JavaScript代码执行过程中，我们学习了很多ECMA文档的术语:

* **执行上下文栈**:Execution Context Stack，用于执行上下文的栈结构;
* **执行上下文**:Execution Context，代码在执行之前会先创建对应的执行上下文
* **变量对象**:Variable Object，上下文关联的VO对象，用于记录函数和变量声明;
* **全局对象**:Global Object，全局执行上下文关联的VO对象;
* **激活对象**:Activation Object，函数执行上下文关联的VO对象
* **作用域链**:scope chain，作用域链，用于关联指向上下文的变量查找;

在新的ECMA代码执行描述中(ES5以及之上)，对于代码的执行流程描述改成了另外的一些词汇:

* 基本思路是相同的，只是对于一些词汇的描述发生了改变，
* 执行上下文栈和执行上下文也是相同的;

# 二、词法环境(Lexical Environments)
词法环境是一种规范类型，用于在词法嵌套结构中定义关联的变量、函数等标识符;

* 一个词法环境是由环境记录(Environment Record)和一个外部词法环境(outer LexicalEnvironment)组成
* 一个词法环境经常用于关联一个**函数声明**、**代码块语句**、**try-catch语句**，当它们的**代码被执行时，词法环境被创建出来;**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731847293000b5rf8e.png)

也就是在ES5之后，执行一个代码，通常会关联对应的词法环境，

* 那么执行上下文会关联哪些词法环境呢?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731847859000mdmd4b.png)
# 三、LexicalEnvironment和VariableEnvironment
LexicalEnvironment用于处理let、const声明的标识符:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17318480690003ynz5x.png)

VariableEnvironment用于处理var和function声明的标识符

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17318480740009a61mm.png)

# 四、环境记录（Environment  Record）
在这个规范中有两种主要的环境记录值:声明式环境记录和对象环境记录，

* 声明式环境记录:声明性环境记录用于定义ECMAScript语言语法元素的效果，如函数声明、变量声明和直接将标识符绑定与ECMAScript语言值关联起来的Catch子句。
* 对象式环境记录:对象环境记录用于定义ECMAScript元素的效果，例如WithStatement，它将标识符绑定与某些对象的属性关联起来。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731848202000nftsql.png)

# 五、新ECMA描述内存图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731848227000czgn8p.png)

