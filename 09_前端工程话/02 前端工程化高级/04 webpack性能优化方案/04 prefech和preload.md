webpack v4.6.0+ 增加了对预获取和预加载的支持。

在声明 import 时，使用下面这些内置指令，来告知浏览器：

 - prefetch(预获取)：将来某些导航下可能需要的资源
 - preload(预加载)：当前导航下可能需要资源

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773218501000q0smsy.png)

与 prefetch 指令相比，preload 指令有许多不同之处：

 - preload chunk 会在父 chunk 加载时，以并行方式开始加载。prefetch chunk 会在父 chunk 加载结束后开始加载。
 - preload chunk 具有中等优先级，并立即下载。**prefetch chunk 在浏览器闲置时下载。**
 - preload chunk 会在父 chunk 中立即请求，用于当下时刻。prefetch chunk 会用于未来的某个时刻。

> [!tip]
> 推荐使用 prefetch


