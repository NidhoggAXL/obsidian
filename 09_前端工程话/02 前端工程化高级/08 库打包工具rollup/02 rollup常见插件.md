
# 一、解决commonjs问题

为什么需要解决commonjs呢？

这个是因为当导出的是commonjs，导入的是ES Module的时候，就会报错。

例如：main.js使用到utile里面的函数，这个时候导入就会报错

```js
// .src/main.js
import { sum } from './utils/sum'
const foo = () => {
  console.log("foo function")
  sum()
}

export {
  foo
}
```

```js
// ./utiles/sum.js
const sum = (num1, num2) => {
  console.log("sum function")
}

module.exports = {
  sum
}
```

执行命令行：

```shell
npx rollup -c
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773499168000zo9zt9.png)

这个时候就需要安装解决commonjs的库：

```shell
npm install @rollup/plugin-commonjs -D
```

再在 rollup.config.js 里面进行配置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773499665000ignmow.png)

# 二、解决第三方库问题

例如一些库在安装的时候，是在 node_modules 里面，如果这个时候引入的这个库是使用 commonjs 来导入的时候就会报错误。

1. 安装lodash

```shell
npm install lodash
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773500116000x9kw2p.png)


2. 入口引入 lodash

```js
import { sum } from './utils/sum'
import _ from 'lodash'//引入lodash
const foo = () => {
  console.log("foo function")
  _.join("abc", "lll")
  sum()
}

export {
  foo
}
```

3. 打包后的错误

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773500061000mhakxv.png)

这个时候需要使用安装解决node_modules的库：

```shell
npm install @rollup/plugin-node-resolve -D
```

这个时候打包得到的结果就会把 lodash 也同时打包到出口文件里面：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773500403000h7hu7d.png)

如果不想打包到 出口文件里面就需要配置：

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773500762000zivu29.png)

# 三、Babel转换代码

我们希望将ES6转成ES5的代码，可以在rollup中使用babel。 

安装rollup对应的babel插件和babel的预设：

```shell
npm install @rollup/plugin-babel @bable/preset-env -D
```

修改配置文件：

 - 需要配置babel.config.js文件；
 - babelHelpers:

```js
// rollup.config.js
const Commonjs = require("@rollup/plugin-commonjs");
const Nodejs = require("@rollup/plugin-node-resolve");
const babel = require("@rollup/plugin-babel");

module.exports = {
  input: "src/main.js",
  output: [
    {
      file: "dist/bundle.umd.js",
      format: "umd", // umd
      name: "myLib", // global variable name
      globals: {
        lodash: "_",
      },
    },
  ],
  external: ["lodash"],
  plugins: [
    Commonjs(),
    Nodejs(),
    babel({
      babelHelpers: "bundled", //  将Babel帮助函数打包到单个文件中，以减少重复代码
      exclude: /node_modules/ //  排除node_modules目录，不对其进行转译
    }),
  ],
};

```


```js
// babel.config.js
module.exports = {
  presets: [
    "@babel/preset-env"
  ]
}
```

# 四、Teser代码压缩

如果我们希望对代码进行压缩，可以使用@rollup/plugin-terser：

```shell
npm install @rollup/plugin-terser -D
```

配置terser：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773566440000k3ax9y.png)

