# 一、处理Vue文件

处理vue文件我们需要使用rollup-plugin-vue插件：

- 但是注意：默认情况下我们安装的是vue3.x的版本，所以我这里指定了一下rollup-plugin-vue的版本；

```shell
npm install vue
```

```shell
npm install rollup-plugin-vue @vue/compiler-sfc -D
```

使用vue的插件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773570748000gbm6zm.png)

# 二、打包vue报错

在我们打包vue项目后，运行会报如下的错误：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17735707780003zhaor.png)

这是因为在我们打包的vue代码中，用到 process.env.NODE_ENV，所以我们可以使用一个插件 rollup-plugin-replace 设置 它对应的值：

```shell
npm install @rollup/plugin-replace -D
```

配置插件信息：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773570974000m1ooad.png)




