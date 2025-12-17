# 一、浏览器和Node.js架构的区别

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765976063000v8cmkb.png)

# 二、Node.js架构

我们来看一个单独的Node.js的架构图：

 - 我们编写的JavaScript代码会经过V8引擎，再通过Node.js的Bindings，将任务放到Libuv的事件循环中；
 - libuv（Unicorn Velociraptor—独角伶盗龙）是**使用C语言编写的库**；
 - libuv提供了**事件循环、文件系统读写、网络IO、线程池**等等内容；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765976104000ksiuhp.png)


