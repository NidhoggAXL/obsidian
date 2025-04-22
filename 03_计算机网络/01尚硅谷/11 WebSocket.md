# 一、认识WebSocket
**使用HTTP 协议，通信只能由客户端发起**

HTTP 协议如何及时获得更新的内容呢?
* HTTP 是请求响应协议

客户端使用轮询方式，隔一段时间发送一次请求
* 导致服务器资源和带宽浪费，且无法及时获取内容

**HTML5 规范中出现了WebSocket 协议**
* 客户端、服务器都可以主动发消息
* 节省服务器资源和带宽，且能够实时通信
* WebSocket 是应用层协议
* 适合用在需要实时通信的应用中

**WebSocket 服务器和客户端之间会维持长连接**

* 连接空闲时开启定时器
* 定时器时间到了，服务器发送一个 Ping 帧
* 如果接收端存活，应该回一个 Pong 帧
* 直没有收到 Pong 则断开连接

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716430405000gt1wfi.png)

HTTP 通信前需要 TCP 握手建立连接

WebSocket 通信前需要 HTTP 帮助建立连接

客户端主动发起 HTTP GET 请求

请求中带上协议升级专用头字段

服务器同意后，响应中也有相应头字段呼应

**WebSocket 头字段：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716430533000gau9sk.png)

