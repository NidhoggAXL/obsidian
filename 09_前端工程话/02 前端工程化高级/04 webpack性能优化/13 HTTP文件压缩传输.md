# 一、什么是HTTP压缩？

HTTP压缩是一种内置在 服务器 和 客户端 之间的，以改进传输速度和带宽利用率的方式；

HTTP压缩的流程什么呢？

第一步：HTTP数据在服务器发送前就已经被压缩了；（可以在webpack中完成）

第二步：兼容的浏览器在向服务器发送请求时，会告知服务器自己支持哪些压缩格式；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773320488000r7wu1m.png)


第三步：服务器在浏览器支持的压缩格式下，直接返回对应的压缩后的文件，并且在响应头中告知浏览器；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773320496000wt6ztt.png)

# 二、目前的压缩格式

compress – UNIX的“compress”程序的方法（历史性原因，不推荐大多数应用使用，应该使用gzip或deflate）；

deflate – 基于deflate算法（定义于RFC 1951）的压缩，使用zlib数据格式封装；

gzip – GNU zip格式（定义于RFC 1952），是目前使用比较广泛的压缩算法；

br – 一种新的开源压缩算法，专为HTTP内容的编码而设计；

# 三、Webpack对文件压缩

webpack中相当于是实现了HTTP压缩的第一步操作，我们可以使用CompressionPlugin。

第一步，安装CompressionPlugin：

```shell
npm install compression-webpack-plugin -D
```

第二步，使用CompressionPlugin即可：

```js
import compressionPlugin = require("compression-webpack-plugin")
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773320647000zwl0e7.png)

