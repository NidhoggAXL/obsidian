DLL是什么呢？

 - DLL全程是动态链接库（Dynamic Link Library），是为软件在Windows中实现共享函数库的一种实现方式；
 - 那么webpack中也有内置DLL的功能，它指的是我们可以**将能够共享，并且不经常改变的代码，抽取成一个共享的库**；
 - 这个库**在之后编译的过程中，会被引入到其他项目的代码中；**

DDL库的使用分为两步:

 - 第一步：打包一个DLL库；
 - 第二步：项目中引入DLL库；

注意：在升级到webpack4之后，React和Vue脚手架都移除了DLL库（下面的vue作者的回复），所以知道有这么一个概念可。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17732248860002f3zb4.png)

