# 一、Vite的安装

首先，我们安装一下vite工具：

```shell
npm install vite –g
npm install vite -d
```

通过vite来启动项目：

```shell
npx vite
```


# 二、Vite对css的支持

vite可以直接支持css的处理：直接导入css即可；

vite可以直接支持css预处理器，比如less

 - 直接导入less；
 - 之后安装less编译器

```shell
npm install less -D
```

vite直接支持postcss的转换： 只需要安装postcss，并且配置 postcss.config.js 的配置文件即可；

```shell
npm install postcss postcss-preset-env -D
```

```js
// postcsst.config.js
module.exports = {
  plugins: [
    require("postcss-preset-env")
  ]
}
```

# 三、Vite对TypeScript的支持

vite对TypeScript是原生支持的，它会直接使用ESBuild来完成编译： 只需要直接导入即可；

如果我们查看浏览器中的请求，会发现请求的依然是ts的文件：

 - 这是因为vite中的服务器Connect会对我们的请求进行转发；
 - 获取ts编译后的代码，给浏览器返回，浏览器可以直接进行解析；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773585585000qg0j8y.png)

> [!note] ts文件里面确实js的代码。

# 四、Vite打包项目

可以直接通过vite build来完成对当前项目的打包工具：

```shell
npx vite build
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773587400000515hda.png)

可以通过preview的方式，开启一个本地服务来预览打包后的效果：

```shell
npx vite preview
```


