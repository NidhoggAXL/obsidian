# 一、什么是Gulp？

什么是Gulp？

 - A toolkit to automate & enhance your workflow；
 - 一个工具包，可以帮你自动化和增加你的工作流；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773491189000bf7ujn.png)

# 二、Gulp和Webpack

gulp的核心理念是task runner

 - 可以定义自己的**一系列任务**，等待任务被执行；
 - 基于**文件Stream**的构建流；
 - 我们可以**使用gulp的插件体系**来完成某些任务；

webpack的核心理念是module bundler

 - webpack是一个**模块化的打包工具**；
 - 可以使用各种各样的**loader来加载不同的模块**；
 - 可以使用各种各样的插件在**webpack打包的生命周期**完成其他的任务；

gulp相对于webpack的优缺点：

 - gulp相对于webpack思想更加的**简单、易用**，更适合编写**一些自动化的任务**；
 - 但是目前对于大型项目（Vue、React、Angular）并不会使用gulp来构建，比如默认gulp是不支持模块化的；


