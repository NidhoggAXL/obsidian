# 一、认识polyfill

Polyfill是什么呢？

 - 翻译：一种用于衣物、床具等的聚酯填充材料, 使这些物品更加温暖舒适；
 - 理解：更像是应该填充物（垫片），一个补丁，可以帮助我们更好的使用JavaScript；

为什么时候会用到polyfill呢？

 - 比如我们使用了一些语法特性（例如：Promise, Generator, Symbol等以及实例方法例如Array.prototype.includes等）
 - 但是某些浏览器压根不认识这些特性，必然会报错；
 - 我们可以使用polyfill来填充或者说打一个补丁，那么就会包含该特性了；

> [!tip] 
> Babel装换的是高级语法，而不是API，比如一些高级的API是不会装换的，比如Promise 就是在有些老的浏览器中根本就不知道。

# 二、如何使用polyfill？

babel7.4.0之前，可以使用 @babel/polyfill的包，但是该包现在已经不推荐使用了：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1772982894000lvxs1i.png)

babel7.4.0之后，可以通过单独引入core-js和regenerator-runtime来完成polyfill的使用：

```shell
npm install core-js regenerator-runtime --save
```

# 三、配置babel.config.js

需要在babel.config.js文件中进行配置，给preset-env配置一些属性：

 - **useBuiltIns**：设置以什么样的方式来使用polyfill；
 - **corejs**：设置corejs的版本，目前使用较多的是3.x的版本
	 - 另外corejs可以设置是否对提议阶段的特性进行支持；
	 - 设置 proposals 属性为true即可；


# 四、useBuiltIns属性设置


第一个值：false

 - 打包后的文件不使用polyfill来进行适配；
 - 并且这个时候是不需要设置corejs属性的；


第二个值：usage

 - 会根据源代码中出现的语言特性，自动检测所需要的polyfill；
 - 这样可以确保最终包里的polyfill数量的最小化，打包的包**相对会小一些**；
 - 可以设置corejs属性来确定使用的corejs的版本；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1772983207000f32l9a.png)

第三个值：entry

 - **如果我们依赖的某一个库本身使用了某些polyfill的特性，但是因为我们使用的是usage，所以之后用户浏览器可能会报错**；
 - 所以，如果你担心出现这种情况，可以使用 entry；
 - 并且需要在入口文件中添加 `import 'core-js/stable'`  和 `import 'regenerator-runtime/runtime'`;
 - 这样做会根据 browserslist 目标导入所有的polyfill，但是**对应的包也会变大**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1772983287000ofcp6y.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1772983290000rb8mpt.png)


