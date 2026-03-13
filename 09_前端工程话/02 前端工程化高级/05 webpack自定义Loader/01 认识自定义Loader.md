# 一、创建自己的Loader

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773386643000g19n0j.png)

Loader是用于对模块的源代码进行转换（处理），之前我们已经使用过很多Loader，比如css-loader、style-loader、babelloader等。

这里来学习如何自定义自己的Loader：

 - Loader本质上是一个**导出为函数的JavaScript模块**；
 - **loader runner库会调用这个函数**，然后将上一个loader产生的结果或者资源文件传入进去；

编写一个hy-loader01.js模块这个函数会接收三个参数：

 - content：资源文件的内容；
 - map：sourcemap相关的数据；
 - meta：一些元数据；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773386624000q1xgyh.png)

在加载某个模块时，引入loader

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17733867980005vhigd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773386824000e4u8io.png)

> [!tip] 注意：
> 传入的路径和context是有关系的，在前面我们讲入口的相对路径时有讲过。


# 二、resolveLoader属性

但是，如果我们依然希望可以直接去加载自己的loader文件夹，有没有更加简洁的办法呢？

 - 配置resolveLoader属性；
 - 这个属性里面的 node_modules 是webpack默认添加的

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773387471000fvd4xn.png)



