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

