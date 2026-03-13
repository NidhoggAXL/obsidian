# 一、什么是Tree Shaking

什么是Tree Shaking呢？

 - Tree Shaking是一个术语，在计算机中表示消除死代码（dead_code）；
 - 最早的想法起源于LISP，用于消除未调用的代码（纯函数无副作用，可以放心的消除，这也是为什么要求我们在进行函数式

编程时，尽量使用纯函数的原因之一）；

 - 后来Tree Shaking也被应用于其他的语言，比如JavaScript、Dart；

# 二、JavaScript的Tree Shaking：

JavaScript的Tree Shaking：

 - 对JavaScript进行Tree Shaking是源自打包工具rollup（后面我们也会讲的构建工具）；
 - 这是因为Tree Shaking依赖于ES Module的静态语法分析（不执行任何的代码，可以明确知道模块的依赖关系）；
 - webpack2正式内置支持了ES2015模块，和检测未使用模块的能力；
 - 在webpack4正式扩展了这个能力，并且通过 package.json的 sideEffects属性作为标记，告知webpack在编译时，哪里文
件可以安全的删除掉；
 - webpack5中，也提供了对部分CommonJS的tree shaking的支持；
	 - https://github.com/webpack/changelog-v5#commonjs-tree-shaking

## 2.1 webpack实现Tree Shaking

事实上webpack实现Tree Shaking采用了两种不同的方案：

 - usedExports：通过标记某些函数是否被使用，之后通过Terser来进行优化的；
 - sideEffects：跳过整个模块/文件，直接查看该文件是否有副作用；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773306822000gwv7bf.png)

## 2.2 usedExports

```js
const foo = () => {
  console.log("foo function exe~")
}
foo()

function minimize() {
  console.log("sum函数")
}

const obj = { name: "axl", age: 19 }
const { name, age } = obj
console.log(name, age)
```

将mode设置为development模式：

 - 为了可以看到 usedExports 带来的效果，我们需要设置为 development 模式
 - 因为在 production 模式下，webpack默认的一些优化会带来很大的影响。

设置usedExports为true和false对比打包后的代码：

 - 在usedExports设置为true时，会有一段注释：unused harmony export mul；
 - 这段注释的意义是什么呢？告知Terser在优化时，可以删除掉这段代码；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773308112000smltd9.png)


这个时候，我们讲 minimize 设置true：

 - usedExports设置为false时，mul函数没有被移除掉；
 - usedExports设置为true时，mul函数有被移除掉；

> [!tip] 
> usedExports实现Tree Shaking是结合Terser来完成的。

## 2.3 sideEffects

sideEffects用于告知webpack compiler哪些模块时有副作用的：

 - 副作用的意思是这里面的代码有执行一些特殊的任务，不能仅仅通过export来判断这段代码的意义；
 - 副作用的问题，在讲React的纯函数时是有讲过的；

在package.json中设置sideEffects的值：

 - 如果我们将sideEffects设置为false，就是告知webpack可以安全的删除未用到的exports；
 - 如果有一些我们希望保留，可以设置为数组；

比如我们有一个format.js、style.css文件：

 - 该文件在导入时没有使用任何的变量来接受；
 - 那么打包后的文件，不会保留format.js、style.css相关的任何代码；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773308953000ock223.png)

## 2. 4 Webpack中tree shaking的设置

如何在项目中对JavaScript的代码进行TreeShaking呢（生成环境）？

 - 在optimization中配置usedExports为true，来帮助Terser进行优化；
 - 在package.json中配置sideEffects，直接对模块进行优化；

# 三、CSS实现Tree Shaking

上面我们学习的都是关于JavaScript的Tree Shaking，那么CSS是否也可以进行Tree Shaking操作呢？

 - CSS的Tree Shaking需要借助于一些其他的插件；
 - 在早期的时候，我们会使用PurifyCss插件来完成CSS的tree shaking，但是目前该库已经不再维护了（最新更新也是在4年前
了）；
 - 目前我们可以使用另外一个库来完成CSS的Tree Shaking：PurgeCSS，也是一个帮助我们删除未使用的CSS的工具；

安装PurgeCss的webpack插件：

```shell
npm install purgecss-webpack-plugin -D
```

## 3.1 配置PurgeCss

配置这个插件（生成环境）：

 - paths：表示要检测哪些目录下的内容需要被分析，这里我们可以使用glob；
 - 默认情况下，Purgecss会将我们的html标签的样式移除掉，如果我们希望保留，可以添加一个safelist的属性；

> [!tip] 
> 可能还需要安装glob，`npm install glob -D`
> resolveApp 其实就是 path.resolve

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773319473000e5tr7t.png)


purgecss也可以对less文件进行处理（所以它是对打包后的css进行tree shaking操作）；

