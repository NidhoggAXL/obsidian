# 一、MiniCssExtractPlugin

MiniCssExtractPlugin可以帮助我们将css提取到一个独立的css文件中，该插件需要在webpack4+才可以使用。

首先，我们需要安装 mini-css-extract-plugin：

```shell
npm install mini-css-extract-plugin -D
```

配置rules和plugins：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773224199000smctq6.png)


> [!tip]
> chunkFilename是对于动态导入的文件分包的名字，例如`import("./style.css")`



