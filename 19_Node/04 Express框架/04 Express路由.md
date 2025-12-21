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

