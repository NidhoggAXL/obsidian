为什么需要使用这个 env 文件呢？

在项目配置的时候，会把一些常数放到 env 的文件里面，方便后面进行修改：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1768054985000gbssui.png)

在 node 中就需要解析这个env文件，这个时候需要下载 dotenv 库：

```bash
npm install dotenv
```


使用过程：

```js
const dotenv = require("dotenv")

dotenv.config()
//  加载环境变量配置文件 dotenv 是一个 Node.js 模块，它从 .env 文件加载环境变量到 process.env 中
// console.log(process.env.SERVER_PROT) //8000

// 从process.env里面解构出来SERVER_PROT，并导出
module.exports = {
  SERVER_PROT
} = process.env

```

> [!tip]
> env 文件是在最外层的文件中，和 package.json 同级文件层。



