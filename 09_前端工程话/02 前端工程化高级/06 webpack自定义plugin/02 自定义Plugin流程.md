# 一、Plugin如何注册

在之前的学习中，我们已经使用了非常多的Plugin：

 - CleanWebpackPlugin
 - HTMLWebpackPlugin
 - MiniCSSExtractPlugin
 - CompressionPlugin
 - 等等。。。

这些Plugin是如何被注册到webpack的生命周期中的呢？

 - 第一：在webpack函数的createCompiler方法中，注册了所有的插件；
 - 第二：在注册插件时，会调用插件函数或者插件对象的apply方法；
 - 第三：插件方法会接收compiler对象，我们可以通过compiler对象来注册Hook的事件；
 - 第四：某些插件也会传入一个compilation的对象，我们也可以监听compilation的Hook事件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773476330000nm4cwn.png)


