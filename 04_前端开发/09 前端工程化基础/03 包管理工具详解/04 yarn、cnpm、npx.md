# 一、yarn工具
另一个node包管理工具yarn： 

* yarn是由**Facebook、Google、Exponent 和 Tilde 联合推出**了一个新的 JS 包管理工具； 
* yarn 是为了弥补 **早期npm** 的一些缺陷而出现的； 
* 早期的npm存在很多的缺陷，比如安**装依赖速度很慢、版本依赖混乱**等等一系列的问题； 
* 虽然从npm5版本开始，进行了很多的升级和改进，但是依然很多人喜欢使用yarn；

yarn和npm命令的一些区别：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174412024300027if5z.png)

# 二、cnpm工具
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744120958000pik9ol.png)


# 三、npx 工具
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17441795560001vuk6a.png)

那么如何使用项目（局部）的webpack，常见的是两种方式： 

**方式一**：明确查找到node_module下面的webpack (在终端中使用如下命令（在项目根目录下）)

```cmd
./node_modules/.bin/webpack --version
```



**方式二**：在 scripts定义脚本，来执行webpack；（本质是查找局部的 webpack）

* 这里定义脚本里面的命令的时候就会优先在局部找 node_modules 里面的 .bin 里面找到可执行命令去执行的，没有了才会去全局里面找。

 ```js
 "scripts": { 
	 "webpack": "webpack --version" 
//npx webpack --version
 }
```


**方式三**：使用npx

```cmd
npx webpack --version
```

npx的原理非常简单，它会到当前目录的`node_modules/.bin`目录下查找对应的命令；

