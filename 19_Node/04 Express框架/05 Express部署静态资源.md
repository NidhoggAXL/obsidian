部署静态资源可以选择很多方式：Node也可以作为静态资源服务器，并且express给我们提供了方便**部署静态资源**的方法；

```js
import express from 'express'

// 开启服务器
const app = express()

// 把uploads文件里面的所有数据进行静态部署
app.use(express.static("./uploads"))

// 监听启动
app.listen(8000)

```

可以在浏览器里面访问静态资源，浏览器会把这个静态资源下载下来，在进行一个展示：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17662386390001fh156.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766238617000ouayfb.png)

这样的话，那么就可以部署前面做过项目的内容了，比如把 爱彼迎 项目进行本地静态部署：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766238815000u1w1km.png)

```js
import express from 'express'

// 开启服务器
const app = express()

// 把dist文件里面的所有数据进行静态部署
app.use(express.static("./dist"))

// 监听启动
app.listen(8000)

```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766238847000t35vze.png)


