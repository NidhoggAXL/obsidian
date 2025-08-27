# 一、为什么要需要babel？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744638256000pnq85l.png)

# 二、Babel命令行使用

babel本身可以作为一个**独立的工具**（和[[06 PostCss工具处理CSS|postcss]]一样），不和webpack等构建工具配置来单独使用。 

如果我们希望在命令行尝试使用babel，需要安装如下库： 

* `@babel/core`：babel的核心代码，必须安装； 
* `@babel/cli`：可以让我们在命令行使用babel；

```bash
npm install @babel/cli @babel/core -D
```

使用babel来处理我们的源代码： 

* src：是源文件的目录； 
* --out-dir：指定要输出的文件夹dist；

```bash
npx babel src --out-dir dist
```


# 三、插件的使用

比如我们需要转换箭头函数，那么我们就可以使用**箭头函数转换相关的插件：**

```bash
npm install @babel/plugin-transform-arrow-functions -D
```

使用的时候：

```bash
npx babel src --out-dir dist --plugins=@babel/plugin-transform-arrow-functions
```


查看转换后的结果：我们会发现 **const 并没有转成 var** 

* 这是因为 plugin-transform-arrow-functions，并没有提供这样的功能；
* 我们需要使用 plugin-transform-block-scoping 来完成这样的功能；

```bash
npm install @babel/plugin-transform-block-scoping -D
```

使用时：

```bash
npx babel src --out-dir dist --plugins=@babel/plugin-transform-block-scoping ,@babel/plugin-transform-arrow-functions
```


# 四、Babel的预设preset

但是如果要转换的内容过多，一个个设置是比较麻烦的，我们可以使用**预设（preset）**： 

* 后面我们再具体来讲预设代表的含义； 

安装@babel/preset-env预设：

```bash
npm install @babel/preset-env -D
```

使用时：

```bash
npx babel src --out-dir dist --presets=@babel/preset-env
```


# 五、babel-loader

在实际开发中，我们通常会在构建工具中通过配置babel来对其进行使用的，比如在webpack中。 

那么我们就需要去安装相关的依赖： 

* 如果之前已经安装了@babel/core，那么这里不需要再次安装；

```bash
npm install babel-loader -D
```

我们可以设置一个规则，在加载js文件时，使用我们的babel：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744638573000ygllyy.png)
# 六、babel-preset

如果我们一个个去安装使用插件，那么需要手动来管理大量的babel插件，我们可以直接给webpack提供一个preset，webpack 会根据我们的预设来加载对应的插件列表，并且将其传递给babel。

比如常见的预设有三个： 

* env 
* react 
* TypeScript

安装preset-env：

```bash
npm install @babel/preset-env
```

	![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744638904000nnobpy.png)

当然也可以把 bable-loader 的配置抽取出来：

创建 bable.config.js 文件：

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744639005000p8ht5m.png)

