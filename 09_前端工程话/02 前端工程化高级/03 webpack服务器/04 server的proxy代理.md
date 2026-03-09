# 一、Proxy代理


proxy是我们开发中非常常用的一个配置选项，它的目的设置代理来解决跨域访问的问题：

 - 比如我们的一个api请求是 http://localhost:9000 ，但是本地启动服务器的域名是 http://localhost:8080 ，这个时候发送网络请求就会出现跨域的问题；
 - 那么我们可以将请求先发送到一个代理服务器，代理服务器和API服务器没有跨域的问题，就可以解决我们的跨域问题了；

我们可以进行如下的设置：

 - **target**：表示的是代理到的目标地址，比如 /api 会被代理到 http://localhost:9000
 - **pathRewrite**：默认情况下，我们的 /api-hy 也会被写入到URL中，如果希望删除，可以使用pathRewrite；
 - **changeOrigin**：它表示是否更新代理后请求的headers中host地址；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773058695000cu71t6.png)


> [!tip]
> 本质也只开启一个本地 node 服务器。

# 二、changeOrigin的解析

这个 changeOrigin官方说的非常模糊，通过查看源码我发现其实是要修改代理请求中的headers中的host属性：

 - 因为我们真实的请求，其实是需要通过 http://localhost:9000 来请求的；
 - 但是因为使用了代理，默认情况下它的值时 http://localhost:8080
 - 如果我们需要修改，那么可以将changeOrigin设置为true即可；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773059237000jb844q.png)

> [!tip]
> 在开发中还是希望配置的，因为你不知道服务器到底有没有校验这个host。
> 服务器校验的原因可能是怕一些人使用node代理服务器来爬取网站的数据，所以会进行一个校验。


服务器获取headers里面的host得到的不同结果：

- 如果开启了changeOrigin ，得到的是 localhost:9000
- 没有开启，就是得到的 localhost:8080


