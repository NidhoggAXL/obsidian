# 一、打包的时间分析

如果我们希望看到每一个loader、每一个Plugin消耗的打包时间，可以借助于一个插件：speed-measure-webpack-plugin

 - 注意：该插件在最新的webpack版本中存在一些兼容性的问题（和部分Plugin不兼容）
 - 截止2021-3-10日，但是目前该插件还在维护，所以可以等待后续是否更新；
 - 我这里暂时的做法是把不兼容的插件先删除掉，也就是不兼容的插件不显示它的打包时间就可以了；

第一步，安装speed-measure-webpack-plugin插件

```shell
npm install speed-measure-webpack-plugin -D
```

第二步，使用speed-measure-webpack-plugin插件

 - 创建插件导出的对象 SpeedMeasurePlugin；
 - 使用 smp.wrap 包裹我们导出的webpack配置；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177332439200079ttm8.png)


# 二、打包后文件分析

## 2.1 方案一：

方案一：生成一个stats.json的文件

```shell
"buiebpack ld:stats": "webpack --config ./config/webpack.common.js --env production --profile --json=stats.json",
```


通过执行npm run build:status可以获取到一个stats.json的文件：

 - 这个文件我们自己分析不容易看到其中的信息；
 - 可以放到 http://webpack.github.com/analyse，进行分析


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773383519000qoeryl.png)

## 2.2 方案二：

方案二：使用webpack-bundle-analyzer工具
 
  - 另一个非常直观查看包大小的工具是webpack-bundle-analyzer。

第一步，我们可以直接安装这个工具：

```shell
npm install webpack-bundle-analyzer -D
```

第二步，我们可以在webpack配置中使用该插件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177338359400048fs8h.png)

在打包webpack的时候，这个工具是帮助我们打开一个8888端口上的服务，我们可以直接的看到每个包的大小。

 - 比如有一个包时通过一个Vue组件打包的，但是非常的大，那么我们可以考虑是否可以拆分出多个组件，并且对其进行懒加载；
 - 比如一个图片或者字体文件特别大，是否可以对其进行压缩或者其他的优化处理；

