# 一、认识rollup

我们来看一下官方对rollup的定义：

 - Rollup is a module bundler for JavaScript which compiles small pieces of code into something larger and more complex, such as a library or application. 
 - Rollup是一个JavaScript的模块化打包工具，可以帮助我们编译小的代码到一个大的、复杂的代码中，比如一个库或者一个应用程序；

我们会发现Rollup的定义、定位和webpack非常的相似：

 - Rollup也是一个模块化的打包工具，但是Rollup主要是针对ES Module进行打包的；
 - 另外webpack通常可以通过各种loader处理各种各样的文件，以及处理它们的依赖关系；
 - rollup更多时候是专注于处理JavaScript代码的（当然也可以处理css、font、vue等文件）；
 - 另外rollup的配置和理念相对于webpack来说，更加的简洁和容易理解；
 - 在早期webpack不支持tree shaking时，rollup具备更强的优势；

目前webpack和rollup分别应用在什么场景呢？

 - 通常在实际项目开发过程中，我们都会使用webpack（比如react、angular项目都是基于webpack的）；
 - 在对库文件进行打包时，我们通常会使用rollup（比如vue、react、dayjs源码本身都是基于rollup的，Vite底层使用Rollup）；


# 二、Rollup基本使用

先安装rollup：

```shell
# 全局安装
npm install rollup -g
# 局部安装
npm install rollup -D

```

创建main.js文件，打包到bundle.js文件中：

> [!tip] f 的意思就是format-格式
> 1. node环境，支持commonjs使用 `-f cjs`
> 2. browser环境，有全局对象使用 `-f iife`
> 3. [[04 AMD和CMD(了解)|AMD]]环境使用 `-f amd`
> 4. UMD所有环境，使用 `-f umd`

```shell
# 打包浏览器的库
npx rollup ./src/main.js -f iife -o dist/bundle.js
# 打包AMD的库
npx rollup ./src/main.js -f amd -o dist/bundle.js
# 打包CommonJS的库
npx rollup ./src/main.js -f cjs -o dist/bundle.js
# 打包通用的库（必须跟上name）
npx rollup ./src/main.js -f umd --name mathUtil -o dist/bundle.js
```

# 三、Rollup的配置文件

需要打包的文件：

```js
const foo = () => {
  console.log("foo function")
}

export {
  foo
}
```

可以将配置信息写到配置文件中rollup.config.js文件：可以对文件进行分别打包，打包出更多的库文件（用户可以根据不同的需求来引入）：

rollup的命令行：

```shell
npx rollup -c
```

rollup.config.js配置文件：

```js
// rollup.config.js
module.exports = {
  input: "src/main.js",
  output: [
    {
      file: "dist/bundle.js",
      format: "cjs", // commonjs
    },
    {
      file: "dist/bundle.es.js",
      format: "es", // es module
    },
    {
      file: "dist/bundle.iife.js",
      format: "iife", // iife
      name: "myLib", // global variable name
    }
  ],
};

```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773498091000aj1hin.png)

