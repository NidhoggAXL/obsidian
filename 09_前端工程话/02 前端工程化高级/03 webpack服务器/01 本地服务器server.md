# 一、为什么要搭建本地服务器？

目前我们开发的代码，为了运行需要有两个操作：

 - 操作一：npm run build，编译相关的代码；
 - 操作二：通过live server或者直接通过浏览器，打开index.html代码，查看效果；

这个过程经常操作会影响我们的开发效率，我们希望可以做到，当文件发生变化时，可以自动的完成 编译 和 展示；

为了完成自动编译，webpack提供了几种可选的方式：

 - webpack watch mode；
 - webpack-dev-server（常用）；
 - webpack-dev-middleware；

# 二、webpack-dev-server

上面的方式可以监听到文件的变化，但是事实上它本身是没有自动刷新浏览器的功能的：

 - 当然，目前我们可以在VSCode中使用live-server来完成这样的功能；
 - 但是，我们希望在不适用live-server的情况下，可以具备live reloading（实时重新加载）的功能；

安装webpack-dev-server

```shell
npm install webpack-dev-server
```

修改配置文件，启动时加上serve参数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773043483000y1fyce.png)


webpack-dev-server 在编译之后不会写入到任何输出文件，而是将 bundle 文件**保留在内存中**： 事实上webpack-dev-server使用了一个库叫memfs（memory-fs webpack自己写的）



