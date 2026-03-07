# 一、npm install 命令

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744117135000x5a7ci.png)


那么全局安装的时候，是如何通过终端的命令行来实现的呢？

可以理解为当我们进行全局安装的时候，会把全局安装的**可执行程序(例如：.exe)配置到电脑的环境变量中。**

当我们在终端中输入时（例如：node）的时候就会**去环境变量**中去寻找配置好的 node **环境变量**，在环境变量中就可以找到含有可执行程序的文件夹，在文件夹里面找到可执行程序并执行。

# 二、项目安装

项目安装会在当前目录下生成一个 node_modules 文件夹，[[03 require函数解析|require]] 查找顺序时有讲解过这个包在什么情况下被 查找； 

局部安装分为开发时依赖和生产时依赖：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744117608000aqfa34.png)


# 二、npm install 原理 

执行 npm install它背后帮助我们完成了什么操作？ 

* 我们会发现还有一个称之为**package-lock.json的文件**，它的作用是什么？ 
* 从npm5开始，**npm支持缓存策略（来自yarn的压力），缓存有什么作用**呢？ 

一幅画出的根据 npm install 的原理图：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174411881300083kntu.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744119100000ckpcng.png)


# 三、package-lock.json

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744118620000qau524.png)


# 四、npm其他命令z

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744119210000nsea1g.png)

npm的命令其实是非常多的： 

* https://docs.npmjs.com/cli-documentation/cli 
* 更多的命令，可以根据需要查阅官方文档

