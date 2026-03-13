什么是Scope Hoisting呢？

 - Scope Hoisting从webpack3开始增加的一个新功能；
 - 功能是对作用域进行提升，并且让webpack打包后的代码更小、运行更快；

默认情况下webpack打包会有很多的函数作用域，包括一些（比如最外层的）IIFE：

 - 无论是从最开始的代码运行，还是加载一个模块，都需要执行一系列的函数；
 - Scope Hoisting可以将函数合并到一个模块中来运行；

使用Scope Hoisting非常的简单，webpack已经内置了对应的模块：

 - 在production模式下，默认这个模块就会启用；
 - 在development模式下，我们需要自己来打开该模块

```js
const webpack = require("webpack")
module.exports = {
  plugins: [
    new webpack.optimize.ModuleConcatenationPlugin()
  ]
}
```

