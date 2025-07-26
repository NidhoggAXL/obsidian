# 一、Node.js是什么
官方对Node.js的定义:

* Node.js是一个**基于V8 JavaScript引擎的JavaScript运行时环境。**

也就是说Node.js基于V8引擎来执行JavaScript的代码，但是不仅仅只有V8引擎:

* 前面我们知道V8可以嵌入到任何C++应用程序中，无论是Chrome还是Node.is，事实上都是嵌入了V8引擎来执行JavaScript代码;
* 但是在Chrome浏览器中，还需要解析、渲染HTML、CSS等相关渲染引擎，另外还需要提供支持浏览器操作的AP1、浏览器自己的事件循环等;
* 另外，在Node.is中我们也需要进行一些额外的操作，比如文件系统读/写、网络I/O、加密、压缩解压文件等操作;

# 二、浏览器和Node.js架构的区别

我们可以简单理解规划出Node.js和浏览器的差异

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743602980000uaobwc.png)


# 三、Node.js架构
我们编写的JavaScript代码会经过V8引擎，再通过Node.js的Bindings，将任务放到Libuv的事件循环中

libuv(Unicorn Velociraptor-独角伶盗龙)是使用C语言编写的库

libuv提供了**事件循环、文件系统读写、网络10、线程池**等等内容

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743602987000zmwyl2.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743681547000829r3n.png)




