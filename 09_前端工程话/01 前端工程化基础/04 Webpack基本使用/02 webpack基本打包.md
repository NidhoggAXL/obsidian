# 一、webpack的默认打包

我们可以通过webpack进行打包，之后运行打包之后的代码：在目录下直接执行 webpack 命令

```bash
webpack
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744206388000w79nk9.png)

生成一个dist文件夹，里面存放一个main.js的文件，就是我们打包之后的文件： 

* 这个文件中的代码被**压缩和丑化**了； 
* 另外我们发现代码中依然存在ES6的语法，比如箭头函数、const等，这是因为默认情况下webpack并不清楚我们打包后的文件是否需要转成ES5之前的语法，后续我们需要**通过babel来进行转换和设置**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744351330000czrq1a.png)


我们发现是可以正常进行打包的，但是有一个问题，webpack是如何确定我们的入口的呢？ 

* 事实上，当我们运行webpack时，**webpack会查找当前目录下的 src/index.js作为入口；** 
* 所以，如果当前项目中**没有存在src/index.js文件，那么会报错；**

当然，我们也可以通过配置来指定入口和出口:

```bash
npx webpack --entry ./src/main.js --output-path ./build
```

# 二、创建局部的webpack

前面我们直接执行webpack命令使用的是全局的webpack，如果希望使用局部的可以按照下面的步骤来操作。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744351610000xjg32c.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744352332000r3qbls.png)






