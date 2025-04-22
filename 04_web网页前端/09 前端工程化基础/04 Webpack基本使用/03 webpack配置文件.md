# Webpack配置文件

在通常情况下，webpack需要打包的项目是非常复杂的，并且我们需要一系列的配置来满足要求，默认配置必然是不可以的。

我们可以在根目录下创建一个`webpack.config.js`文件，来作为webpack的配置文件：

* entry(入口)：确定 webpack 在进行打包时查找的入口
* output(出口)：
	* filenname:确定导出文件的文件名
	* path：确定导出的位置(必须是[[00 前言#^b867a8|绝对路径]])

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744352652000dfr5kg.png)

进行打包的时候使用`webpack.config.js`配置文件来进行打包：继续执行webpack命令，依然可以正常打包：`npm run build`

* 可以我也是可以指定使用的配置文件的，但是默认不指定打包配置的文件的时候
* webpack会默认找到当前目录下面 webpack.config.js 进行配置，并打包 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17443534160002vrq3a.png)

# 指定配置文件
但是如果我们的配置文件并不是 webpack.config.js 的名字，而是其他的名字呢？ 

* 比如我们将webpack.config.js修改成了 aoao.config.js； 
* 这个时候我们可以通过 --config 来指定对应的配置文件；

不适用默认的文件名，改变文件名来打包：使用命令`npx webpack --config ./aoao.config.js`


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744353600000oe40tg.png)


每次这样编译，会比较繁琐也可以在 package.json 中增加一个脚本：使用 `npm run build` 打包。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17443538170002opuzs.png)


# webpack的依赖图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17443547190005z6qym.png)

