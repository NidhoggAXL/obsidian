# 一、Webpack和Tapable

知道webpack有两个非常重要的类：Compiler和Compilation

 - 他们通过注入插件的方式，来监听webpack的所有生命周期；
 - 插件的注入离不开各种各样的Hook，而他们的Hook是如何得到的呢？
 - 其实是创建了Tapable库中的各种Hook的实例；

所以，如果我们想要学习自定义插件，最好先了解一个库：Tapable

 - Tapable是官方编写和维护的一个库；
 - Tapable是管理着需要的Hook，这些Hook可以被应用到我们的插件中；

# 二、Tapable有哪些Hook呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177341207700018aonw.png)

# 三、Tapable的Hook分类

同步和异步的：

 - 以**sync**开头的，是同步的Hook；
 - 以**async**开头的，两个事件处理回调，不会等待上一次处理回调结束后再执行下一次回调；

其他的类别

 - bail：当有返回值时，就不会执行后续的事件触发了；
 - Loop：当返回值为true，就会反复执行该事件，当返回值为undefined或者不返回内容，就退出事件；
 - Waterfall：当返回值不为undefined时，会将这次返回的结果作为下次事件的第一个参数；
 - Parallel：并行，会同时执行次事件处理回调结束，才执行下一次事件处理回调；
 - Series：串行，会等待上一是异步的Hook；

