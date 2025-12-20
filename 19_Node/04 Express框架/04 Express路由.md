# 一、认识Express路由

如果我们将所有的代码逻辑都写在app中，那么app会变得越来越复杂：

 - 一方面完整的Web服务器包含非常多的处理逻辑；
 - 另一方面有些处理逻辑其实是一个整体，我们应该将它们放在一起：比如对users相关的处理
	 - 获取用户列表；
	 - 获取某一个用户信息；
	 - 创建一个新的用户；
	 - 删除一个用户；
	 - 更新一个用户；

我们可以使用 express.Router来创建一个路由处理程序：

 - 一个Router实例**拥有完整的中间件和路由系统**；
 - 因此，它也被称为 **迷你应用程序（mini-app）**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766237965000b20mqu.png)

# 二、静态资源服务器

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


