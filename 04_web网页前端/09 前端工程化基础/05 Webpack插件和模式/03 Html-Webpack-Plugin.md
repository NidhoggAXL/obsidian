# 插件基本使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17447193650000nol2n.png)

# 生成index.html分析
我们会发现，现在自动在dist文件夹中，生成了一个index.html的文件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17447201230002llp1n.png)

该文件中也自动添加了我们打包后的 **.js** 文件；[[05 script的defer和async属性#一、defer属性|defer]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17447200640006c07mb.png)

这个文件是如何生成的呢？ 

* 默认情况下是根据 **ejs** 的一个模板来生成的；
* 在html-webpack-plugin的源码中，有一个default_index.ejs模块；

# 自定义HTML模板
如果我们想在自己的模块中加入一些比较特别的内容：

* 比如添加一个**noscript标签**，在用户的JavaScript被关闭时，给予响应的提示； 
* 比如在**开发vue或者react项目时**，我们需要一个可以挂载后续组件的根标签；

这个我们需要一个属于自己的index.html模块：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744720403000f1mpoh.png)

# 自定义模板数据填充
上面的代码中，会有一些类似这样的语法`<% 变量 %>`，这个是**EJS模块填充**数据的方式。

在配置HtmlWebpackPlugin时，我们可以添加如下配置： 

* template：指定我们要使用的模块所在的路径；
* title：在进行htmlWebpackPlugin.options.title读取时，就会读到该信息；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744720446000jo9msr.png)

