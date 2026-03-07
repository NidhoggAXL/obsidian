# 一、认识PostCSS工具

可以借助于构建工具： 

* 在webpack中使用postcss就是使用postcss-loader来处理的；

安装postcss-loader： 

```bash
npm install postcss-loader -D
```

我修改加载css的loader：（配置文件已经过多，给出一部分了） 
* 注意：因为postcss需要**有对应的插件**才会起效果，所以我们需要配置它的plugin；
* 这里就是一个完整的 [[04 编写和打包CSS文件#四、loader配置方式|loader]] 的配置方式

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744552929000jcsax2.png)

比如在使用 webpack 打包工具后的 `user-select: none;` 属性，在有些浏览器中不适配的需要添加前缀，这里我们就可以使用 postcss 的 autoprefixer 来添加前缀

> [!note] autoprefixer 也需要进行安装(下一节有讲)
>  * autoprefixer 就是 postcss的插件



![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744553512000f2l5mu.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744553565000mkcf4r.png)


# 二、单独的postcss配置文件

因为我们需要添加前缀，所以要安装 autoprefixer：

```bash
npm install autoprefixer -D
```

我们可以将这些**配置信息**放到一个单独的文件中进行管理： 

* 在**根目录下**创建postcss.config.js

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744553228000bhft2n.png)

这个时候在 webpack.config.js 中就不用把 postcss 的配置信息放到那里了：

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744553323000jv6o17.png)


# 三、postcss-preset-env

事实上，在配置postcss-loader时，配置插件并不需要使用 **autoprefixer**。

可以使用另外一个插件：postcss-preset-env 

* postcss-preset-env**也是一个postcss的插件；** 
* 它可以帮助我们将一些现代的CSS特性，**转成大多数浏览器认识的CSS**，并且会根据目标浏览器或者运行时环境**添加所需的 polyfill**； 
* 也包括会自动帮助我们添加autoprefixer（所以相当于已经内置了autoprefixer）；

安装postcss-preset-env：

* porset-预设
* env-环境

```bash
npm install postcss-preset-env -D
```

之后，直接修改掉之前的autoprefixer即可：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744554026000a93wwm.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17445540340004kae46.png)

