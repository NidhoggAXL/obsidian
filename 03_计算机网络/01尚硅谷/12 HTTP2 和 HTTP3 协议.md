# 一、HTTP1.1 的不足和优化
**不足：**

* 同一时间，一个连接只能被一个请求/响应使用
	* 现在浏览器可以同时建立6个连接，连接过多对服务器开销较大
* 对其它资源的请求/响应想使用连接必须排队
* 多次请求/响应中，头信息重复传输
	* 如果 Cookie 很多，开销更大

什么是Cookie？

> 在计算机中，Cookie（小甜饼）是一种小型文本文件，由Web服务器创建并存储在用户的计算机上。Cookie通常用于存储用户的个人信息、偏好设置或其他数据，以便在用户下次访问同一网站时可以快速检索和使用这些信息。
> 
> Cookie通常由名称、值和过期时间组成。名称是Cookie的唯一标识符，值是存储在Cookie中的数据，而过期时间是Cookie的有效期限。当用户访问某个网站时，该网站的服务器可以在用户的计算机上创建或更新Cookie，然后在用户下次访问该网站时，服务器可以读取Cookie中的信息，以提供个性化的服务或记录用户的行为。
> 
> Cookie有不同的类型，包括会话Cookie（Session Cookie）、持久Cookie（Persistent Cookie）和第三方Cookie（Third-party Cookie）。会话Cookie是在用户关闭浏览器时自动删除的，而持久Cookie则可以长期存储在用户的计算机上。第三方Cookie是由其他网站创建的Cookie，用于跟踪用户的行为或提供个性化的服务。

**优化：**

* 可以将一些静态资源放置到不同的域名下
	* 每个域名都可以建立多个连接
* 发送更少的请求
	* 把多个js 或 css 合并成一个文件
		* 但是如果小文件发生了更改，大文件也要进行更改
	* Sprite 图，将多张图片合并成一张更大的图片
		* 小图片变化大图标也会变化
	* 将 css、js 或图片直接内联到 HTML中
		* css、js有缓存的，如果内联到 HTML 中就没有内联了
		* 没有缓存就会减少速度

# 二、HTTP2 协议
针对 HTTP1.1 的不足进行改进和优化，就有了 HTTP2 协议

HTTP2 在底层做了很多改进和优化，但在语义上兼容 HTTP1.1

升级到 HTTP2，客户端和服务器端几乎不需要修改代码

升级到 HTTP2，需要浏览器和服务器都支持

浏览器要求 HTTP2 必须基于 SSL/TLS

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716431515000e51bn4.png)


**HTTP2 协议的设计：**

* 所有的请求/响应都可以在一个 TCP 连接上完成
* **以帧(frame)的方式传输数据**
* 把首部封装成首部帧，主体部分封装成数据帧，每个帧都有标识符
* 不同请求/响应的帧可以在 TCP 连接上交错传输，接收后根据标识符组装
* 请求和对应的响应使用相同的标识符ID

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716431854000u7lgnt.png)

> 帧有最大传输单位，当超过的时候就会进行分片的操作，分片后又标志位来进行判断后面是否还有分片

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716432109000wq67wd.png)

* Priority：表示优先级
* Headers：标识headers这个首部帧后面还有首部帧吗？
	* 有的话为 0，没有的话为 1
	* 没有的话后面就要开始接受数据帧了
* Stream：标识流是否结束了，结束为1
	* 这里的流是一个抽象的概念，标识一个完整的请求或者一个完整的响应。
	* 一个流里面多多个帧，比如 Headers帧、数据帧
* Stream Identifier：流标识符
	* 接受端就可以根据标识符来吧帧组装起来

## 2.1 HTTP2 的多路复用和首部压缩

**多路复用**


* 可以并行交错地发送请求，请求之间互不影响
* 可以并行交错地发送响应，响应之间互不干扰
* 只使用一个连接即可并行发送多个请求和响应
* 解决了 HTTP1.1 中请求过多时需要排队等待的问题

**优先级**


*  请求/响应不用排队，可以立刻发送，可能导致带宽浪费在非关键资源上
* 影响渲染的 CSS、JS(关键资源)就比异步 JS 和图片等(非关键资源)关键
* 需要保证关键资源优先处理
* 因此 HTTP2 引入了优先级机制，保证优先处理优先级更高的请求
* 浏览器优先发送高优先级的请求，服务器会给高优先级的请求发送更多帧

## 2.2 HTTP2 首部压缩 

* 首部很臃肿，相似的字段，巨长的 Cookie，每次都传输首部，非常浪费
* HTTP2 采用了 HPACK 压缩算法，对首部进行了压缩
* 客户端和服务器都保存一张静态只读表，对常用字段(头、值)索引
* 如果字段在表中能找到，直直接使用索引替代，接收方根据静态表还原

**静态表：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716432862000wvr87t.png)

> cookie 在每个不同的 URL 中不一样的，但是头部一样
> 所以 cookie 的头部可以放在静态表中，数据部分放到动态表中

**动态表：**

* 客户端和服务器通过通信方式，维护一张动态表
* 如果字段名和值都在静态表中，直接使用索引
* 如果只有字段名在静态表中，名使用索引，值可以采用 Huffman 编码
	* Huffman 是一种编码方式（可变长编码），常用的字符使用短编码，不常用的使用长编码
* 可以将重复传输的字段名和值保存在动态表中，对其进行索引
* 再次传输时，如果在表(静态和动态表)中，直接使用索引

**HTTP2 传输过程中静态表和动态表的使用：**

第一次传输：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716433368000nswefi.png)

动态表发生更新：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716433390000q718em.png)

再次进行传输：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716433443000ibhfy1.png)


**抓包HTTP2 :**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17164335990000yolpr.png)

这里的`:method GET`在静态表中不是 2 为什么这里前面还有一个8，这是为了在后面解析的时候方便知道解析成什么，是属于一种控制的作用，所以在实际传输的时候不只是会传输索引的值，还会传输控制的值。

> [!tip] 控制的作用：
> 把这个字符存储到动态表中或者到静态表中找到索引等。

**看一下二进制**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716433797000vv8j3l.png)

> 这里看到的二进制是一个字符8个字节，2个16进制数
> 前4为表示 8
> 后4为表示 2

## 2.3 HTTP2 的服务器推送（了解）
服务器可以对客户端的一个请求发送多个响应

可以推送额外资源，而无需客户端明确地请求

* 比如客户端请求首页 HTML，解析 HTML后，一般还会请求CSS、JS 等

服务器收到获取HTML的请求，在响应HTML后，主动推送CSS等资源


# 三、HTTP3 协议
**HTTP2 的不足：**

* HTTP2 基于 TCP+SSL/TLS

* 连接建立的过程中握手过多、慢启动，消耗的时间太长

* IP 地址变化，TCP连接无法维持，对移动设备支持不好
	* 移动端如果发生了网络的变化 IP 是会发生变化的
	* 比如 4G 切换到 5G 的过程
	* 这是 TCP 的问题，HTTP2 无能为力
* 还有队头阻塞问题:前面的数据未到达，导致后面的数据无法交付
	* 这也是 TCP 可靠传输的问题，HTTP2 也无能为力
	* 那该怎么办呢?是时候抛弃 TCP 协议了

**HTTP3 的改进：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17164347730000mwg2b.png)

* HTTP3 放弃了 TCP 协议，改为使用 UDP 协议
* UDP 不提供可靠传输、拥塞控制、流量控制等功能
* 在 UDP 和应用层之间新增一层 QUIC 协议
* 在 QUIC 协议中实现相关功能

**QUIC 协议：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17164349980004votms.png)


* 将 HTTP2 的一些好特性移到 QUIC 协议中
* 在 QUIC 中重新高效实现 TCP 中的部分功能
* 借助 TLS1.3 解决安全传输的问题
* 基于 UDP 在 QUIC 中实现连接迁移等新特性

