# 一、Node程序传递参数

正常情况下执行一个node程序，直接跟上我们对应的文件即可

```bash
node index.js
```

但是，在某些情况下执行node程序的过程中，我们可能希望给node传递一些参数:

```bash
node index.js (env=development coderwhy)-传递的参数
```

如果我们这样来使用程序，就意味着我们需要在程序中获取到传递的参数:

* 获取参数其实是在**process的内置对象中**的;
* 如果我们直接打印这个内置对象，它里面包含特别的信息:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743687198000e3drnn.png)


现在，我们先找到其中的argv属性-argvector (向量-容器):

* 我们发现它是一个数组，里面包含了我们需要的参数，

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743687296000zzuo6w.png)

> [!tip] 为什么叫argv呢？
> 在C/C++程序中的main函数中，实际上可以获取到两个参数:
>* **argc**:argument counter的缩写，传递参数的个数;
>* **argv**:argument vector(向量、矢量)的缩写，传入的具体参数。
>	* vector翻译过来是矢量的意思，在程序中表示的是一种数据结构。
>	* 在C++、Java中都有这种数据结构，是一种数组结构;
>	* 在JavaScript中也是一个数组，里面存储一些参数信息;


# 二、Node的输出

console.log（掌握这个，其他了解）

* 最常用的输入内容的方式:console.log

console.clear

* 清空控制台:console.clear

console.trace

* 打印函数的调用栈:console.trace

还有一些其他的方法，其他的一些console方法，可以自己在下面学习研究一下： https://nodejsorg/dist/latest-v16.x/docs/api/console.html

# 三、Node的REPL(了解)

什么是REPL呢?感觉挺高大上

* REPL是Read-Eval-Print Loop的简称，翻译为“读取-求值-输出”循环
* REPL是一个简单的、交互式的编程环境事实上，我们**浏览器的console就可以看成一个REPL**。

事实上，我们浏览器的console就可以看成一个REPL。

Node也给我们提供了一个REPL环境，我们可以在其中演练简单的代码。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743747324000dm36d8.png)

