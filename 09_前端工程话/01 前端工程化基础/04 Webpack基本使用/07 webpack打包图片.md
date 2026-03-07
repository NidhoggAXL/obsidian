# 一、加载图片案例准备

为了演示我们项目中可以加载图片，我们需要在项目中使用图片，比较常见的使用图片的方式是两种： 

* img元素，设置src属性； 
* 其他元素（比如div），设置background-image的css属性；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174463329600033sox8.png)

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744633303000427tvn.png)

> [!warning] 这个时候打包会出现错误，webpack不可以正确的打包文件。

# 二、认识asset module type

我们当前使用的webpack版本是webpack5： 

* 在webpack5之前，加载这些资源我们需要使**用一些loader，比如raw-loader 、url-loader、file-loader**
* 在webpack5开始，我们可以直接使用**资源模块类型（asset module type）**，来替代上面的这些loader

在使用的时候先要确定好我们的 loader 中test的属性值：

```js
test:/\.(png|svg|jpe?g|gif)$/i
. 需要转义所以添加 \
? 表示1个或者0个
```

资源模块类型(asset module type)，通过添加 4 种新的模块类型，来替换所有这些 loader： 

## 2.1 asset/resource

 asset/resource 发送一个单独的文件并导出 URL。 
* 之前通过使用 file-loader 实现；

打包后的文件：（会把图片进行哈希算法重新命名，并打包到文件中）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174463383900076tlb8.png)

网页中的显示样子：（图片以url的形式在网页中被网络请求显示）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744633941000x6yv4t.png)

## 2.2 asset/inline

 asset/inline 导出一个资源的 data URI。 
* 以前通过使用 url-loader 实现； 

打包后文件：（会把图片转换为代码的格式嵌入到打包的 js 文件中)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744634051000plf97o.png)

网页中的显示样子：(可以看出是**一种使用 base64 的算法进行格式为浏览器认识的代码**，这样就可以显示到页面)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744634124000yn9srx.png)


## 2.3 asset/source(舍弃)

asset/source 导出资源的源代码 
* 以前通过使用 raw-loader 实现； 

现代的浏览器已经**不在识别这种的打包格式**：（虽然可以打包）

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744634380000709hyr.png)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744634389000zidn0n.png)

## 2.4 asset(开发使用)

asset 在导出一个 data URI 和发送一个单独的文件之间**自动选择**。
* 之前通过使用 url-loader，并且配置资源体积限制实现；

结果和 asset/rersource ：

这样因为我们的图片少，并且图片的大小没有太大的区别，当图片的大小区别很大的时候就可以看出打包的过程中是进行了选择的。

# 三、asset module type的使用

如何可以自定义文件的输出路径和文件名呢？ 

* 方式一：修改output，添加assetModuleFilename属性； 

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744634794000h1rljh.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744634897000zg3dr7.png)


> [!tip]
> 这样存在一个问题，这是所有的 asset 的导出口确定，如果后面还有别的关于 asset 的文件也会打包到这个文件里面


* 方式二：在Rule中，添加一个generator属性，并且设置filename；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17446352270008bsf56.png)

 > [!note] **这样的好处是**：符合 test 的资源才会打包到这个文件里面

我们这里介绍几个最常用的**placeholder（占位符）**： 

* `[ext]`： 处理文件的扩展名； 
	* 扩展名是自带点`.`的所以路径里面没有点
* `[name]`：处理文件的名称； 
* `[hash]`：文件的内容，使用MD4的散列函数处理，生成的一个128位的hash值（32个十六进制）；
	* `[hash:6`是区前面 6 位使用

> [!note] `img/`是创建一个 img 文件夹来存放后面占位符所表示的文件


# 四、url-loader的limit效果

开发中我们往往是**小的图片需要转换**，但是**大的图片直接使用图片即可** 

* 这是因为**小的图片转换base64**之后可以和**页面一起被请求**，**减少不必要的请求过程；** 
* 而**大的图片也进行转换**，反而会**影响页面的请求速度**；

我们需要两个步骤来实现： 

* 步骤一：将type修改为asset； 
* 步骤二：添加一个 **parser(解析器)** 属性，并且制定**dataUrl的条件**，添加maxSize属性；
	* condition(条件)

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744635839000xiu34n.png)


这样小于 100kb 的图片转换 base64 和页面一起请求
* maxSize 是使用字节(byte)为单位
* 1kb = 1024byte
* `100kb = 100 * 1024`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744635820000rpcrea.png)

