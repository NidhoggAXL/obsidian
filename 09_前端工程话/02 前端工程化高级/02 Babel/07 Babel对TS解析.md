# 一、TypeScript的编译


在项目开发中，我们会使用TypeScript来开发，那么TypeScript代码是需要转换成JavaScript代码。

可以通过TypeScript的compiler来转换成JavaScript：

```shell
npm install typescript -D

```

另外TypeScript的编译配置信息我们通常会编写一个tsconfig.json文件：

```shell
tsx --init
```

生成配置文件如下：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17730410580000jkdew.png)


之后我们可以运行 npx tsc来编译自己的ts代码：

```shell
npx tsc
```

# 二、使用ts-loader

如果我们希望在webpack中使用TypeScript，那么我们可以使用ts-loader来处理ts文件：

```shell
npm install ts-loader -D
```

配置ts-loader：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773041486000wm760c.png)

之后，我们通过npm run build打包即可。

# 三、使用babel-loader

除了可以使用TypeScript Compiler来编译TypeScript之外，我们也可以使用Babel：

 - Babel是有对TypeScript进行支持；
 - 我们可以使用插件： @babel/tranform-typescript；
 - 但是更推荐直接使用preset：@babel/preset-typescript；

安装@babel/preset-typescript：

```shell
npm install @babel/preset-typescript -D
```

babel.config.js 配置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773041750000utwcmt.png)

webpack.config.js 里面的rule配置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773041778000f19y35.png)


# 四、ts-loader和babel-loader选择

那么我们在开发中应该选择ts-loader还是babel-loader呢？

使用ts-loader（TypeScript Compiler）

 - 来直接编译TypeScript，那么只能将ts转换成js；
 - 如果我们还希望在这个过程中添加对应的[[05 babel和polyfill|polyfill]]，那么ts-loader是无能为力的；
 - 我们需要借助于babel来完成polyfill的填充功能；

使用babel-loader（Babel）

 - 来直接编译TypeScript，也可以将ts转换成js，并且可以实现polyfill的功能；
 - 但是babel-loader在编译的过程中，**不会对类型错误进行检测**；

那么在开发中，我们如何可以同时保证两个情况都没有问题呢？

# 五、编译TypeScript最佳实践

事实上TypeScript官方文档有对其进行说明：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773042081000k0ivig.png)

也就是说我们使用Babel来完成代码的转换，使用tsc来进行类型的检查。

但是，如何可以使用tsc来进行类型的检查呢？

 - 在这里，我在scripts中添加了两个脚本，用于类型检查；
 - 我们执行 npm run type-check 可以对ts代码的类型进行检测；
 - 我们执行 npm run type-check-watch 可以实时的检测类型错误；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773042311000bg0m98.png)


