webpack的导出大多时候都是一个对象

```js
module.exports = {
 mode: "development"
}
```

但是也可以导出一个函数，当webpack发现你导出的是一个函数的时候，就会执行这个函数

```js
module.exports = function () {
  console.log("webpack导出")
}
```


那这个有什么用呢？当我们在启动webpack的时候可以进行设置

```shell title="设置生成环境"
webpack --config ./config/comm.config.js --env production
```

```shell title="设置开发环境"
webpack --config ./config/comm.config.js -env development
```

这样就可以在导出的时候获取到 env 设置的环境

```js
import commonConfig from ("./config/comm.js")
module.exports = function (env) {
  console.log(env)//可以获取到env设置的变量
  return commonConfig;
}
```

如果是存在3个配置文件：

- `comm.config.js`放入公共的配置代码
- `development.config.js`开发环境的配置代码
- `production.config.js`生成环境配置的代码

现在知道了可以通过导出函数来确定不同的环境，但是需要把公共配置和环境配置结合的话就需要使用到一个插件，webpack-merge 来使用：

安装：

```shell
npm install webpack-merge -D
```

使用：这样在不同的环境下面使用不同的配置

```js
import commConfig from "./config/comm.config.js"//公共配置
import devConfig from "./config/development.config.js"//开发配置
import proConfig from "./config/production.config.js"//生产配置
import { merge } from "webpack-merge"

module.exports = function(env) {
  const isProduction = env.production
  let mergeConfig = isProduction ? proConfig : devConfig
  return merge(commConfig, mergeConfig)
}
```



