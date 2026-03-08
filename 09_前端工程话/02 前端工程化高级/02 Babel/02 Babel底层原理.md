# 一、原理

babel是如何做到将我们的一段代码（ES6、TypeScript、React）转成另外一段代码（ES5）的呢？

 - 从一种源代码（原生语言）转换成另一种源代码（目标语言），这是什么的工作呢？
 - 就是编译器，事实上我们可以将babel看成就是一个编译器。
 - Babel编译器的作用就是将我们的源代码，转换成浏览器可以直接识别的另外一段源代码；

Babel也拥有编译器的工作流程：

 - 解析阶段（Parsing）
 - 转换阶段（Transformation）
 - 生成阶段（Code Generation）

babel中这个转换过程，也是babel的作者：https://github.com/jamiebuilds/the-super-tiny-compiler


# 二、babel编译器执行原理

Babel的执行阶段

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17729711130009960uc.png)


当然，这只是一个简化版的编译器工具流程，在每个阶段又会有自己具体的工作：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1772971123000xbjma4.png)

