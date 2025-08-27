# 一、如何处理less文件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744548937000894q6u.png)


# 二、fLess工具处理

我们可以使用less工具来完成它的编译转换

```
npm install less -D
```

执行如下命令：

```
npx lessc 转换文件.less 转换后的文件.css
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17445493520009zvmti.png)


# 三、less-loader处理

但是在项目中我们会编写大量的css，它们如何可以自动转换呢？

* 这个时候我们就可以使用 less less-loader，来自动使用less工具转换less到css；
* 如果没有安装 less 的时候就在需要安装 less

```
npm install less less-loader -D
```

配置到 webpack.config.js 

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174454990700013q7bk.png)

执行 `npx webpack`进行打包，less就会自动装换为打包好的css，页面也会自动生效。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744550069000tfqy5m.png)




