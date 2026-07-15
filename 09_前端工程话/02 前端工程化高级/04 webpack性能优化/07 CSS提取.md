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


# 二、 Hash、ContentHash、ChunkHash

在我们给打包的文件进行命名的时候，会使用placeholder，placeholder中有几个属性比较相似：

 - hash、chunkhash、contenthash
 - hash本身是通过**MD4的散列函数**处理后，生成一个128位的hash值（32个十六进制）；
## 2.1 核心区别（装修大楼的比喻）

- **`[hash]`（整栋楼的指纹）**：代表**整个项目（Compilation）**的哈希值。只要你修改了项目中**任何一个**文件（哪怕是一个注释），整栋楼的指纹都会变，所有打包出来的文件名称都会跟着变。
    
    - _后果_：改了 1 个 JS 文件，导致图片、CSS 等所有文件的缓存都失效，浏览器得全部重新下载。**不推荐用于生产环境**。
        
- **`[chunkhash]`（每一层的指纹）**：代表**每一个代码块（Chunk）**的哈希值。它根据入口文件及其依赖的模块计算。比如 `app.js` 和 `vendor.js` 是两个不同的 chunk，改业务代码只会影响 `app` 的 chunkhash，`vendor` 不受影响。
    
    - _局限_：如果在 JS 中引入了 CSS（使用 `style-loader` 或 MiniCssExtractPlugin），CSS 和 JS 属于同一个 Chunk。改 CSS 会导致 JS 的 chunkhash 也改变，导致 JS 缓存失效，这并不完美。
        
- **`[contenthash]`（每个房间的指纹）**：代表**文件具体内容**的哈希值。它完全基于文件自身的二进制内容计算。只要这个文件的内容没变，哈希就绝对不变。
    
    - _优势_：**最精确**。修改 CSS 文件，只有 CSS 的 contenthash 改变，JS 文件的哈希纹丝不动。**这是现代 Webpack 生产环境配置的首选。**

## 2.2 使用

通常在 `output.filename`（入口文件）和  MiniCssExtractPlugin（抽离的 CSS 文件）中配置。

```js
// webpack.config.js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  // 入口文件输出配置
  output: {
    // 推荐使用 [contenthash] 给 JS 文件命名
    filename: '[name].[contenthash:8].js', 
    // 异步加载的 chunks 同样使用 contenthash
    chunkFilename: '[name].[contenthash:8].chunk.js',
    clean: true, // 打包时清理旧文件
  },
  plugins: [
    new MiniCssExtractPlugin({
      // 抽离出的 CSS 文件，一定要用 contenthash（千万别用 chunkhash）
      filename: '[name].[contenthash:8].css',
      chunkFilename: '[name].[contenthash:8].css',
    }),
  ],
};
```

> [!tip] 
> **注意**：`[contenthash:8]` 代表取哈希值的前 8 位，让文件名更短。



