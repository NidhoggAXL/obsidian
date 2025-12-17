
**官方对Node.js的定义**：Node.js是一个基于V8 JavaScript引擎的JavaScript运行时环境。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765975963000k5z70t.png)


也就是说Node.js基于V8引擎来执行JavaScript的代码，但是**不仅仅只有V8引擎**：

 - 前面我们知道V8可以嵌入到任何C ++应用程序中，无论是Chrome还是Node.js，事实上都是嵌入了V8引擎来执JavaScript代码；
 - 但是在Chrome浏览器中，还需要解析、渲染HTML、CSS等相关渲染引擎，另外还需要提供支持浏览器操作的API、浏览器自己的事件循环等；
 - 另外，在Node.js中我们也需要进行一些额外的操作，比如**文件系统读/写、网络IO、加密、压缩解压文件等操作**；

