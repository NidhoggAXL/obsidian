# 一、基础 TCP 协议的通信
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715860212000kw1xtr.png)

**使用 Node.js 实现 TCP 协议连接**

**通过代码加强对 TCP 协议的理解**

**理解客户端如何发送和接收数据**

**理解服务器端如何发送和接收数据**

客户端一般指客户端程序，是主动发起连接的一方

服务端一般指服务器程序，用来处理不同客户端的连接

服务器启动后会占用固定端口号，等待着客户端的连接

客户端和服务器建立 TCP 连接后即可开始互相发送和接收数据

客户端和服务器都可以主动断开连接

1. 创建两个 js 文件，一个 server（服务器）、clients（客户端）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715861159000fxn2rr.png)

2. 对 server.js 进行配置

```node.js
// 导入 node 内置模块
// 可用于 TCP 通信
const net = require('net')
  
// 创建 TCP 服务器
const server = net.createServer()

// 监听固定端口
// 127.0.0.1 用于测试的端口号
// 在本机可以通过 127.0.0.1:9000 或者localhost:9000 访问本服务器
server.listen(9000,'127.0.0.1',function(){
    console.log('服务器已在 127.0.0.1:9000 启动')
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158612020001h7yjd.png)

3. 在终端启动 server 并启动服务器

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158612570007ovec6.png)

4. 对客户端进行导入，并终端打开，但是不运行，为后面抓包准备

```node.js
// 导入 node 内置模块
// 可用于 TCP 通信
const net = require('net')

// 创建客户端连接，目标 172.0.0.1:9000 服务器
const client = net.createConnection({
    host:'127.0.0.1',port:9000
})

// 客户端不需要像服务器一样绑定具体的端口号，使用随机端口号
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158619440008i6prp.png)

5. 打开抓包软件，并运行 client 代码进行抓包

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158627710006ewvc6.png)

建立了连接双方就可以发送和接受数据了。

但是上面的代码还是不可以确定已经建立了连接，建立连接不是代码运行了就建立了连接。

6. node.js 中通过事件来确认连接成功了。

* 要修改代码，所以要停止服务，服务器或者客户端都可以在命令行输入`Ctrl+c`就可以停止服务了。
* 修改完代码在开启服务器和客户端的连接`node server/client.js`
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715863289000llvhxb.png)

* 再次进行抓包
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715863521000dmjq6p.png)

7. 那服务器端如何确认是和谁连接了呢？

* 要修改代码，操作和上面一样
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864437000jd0m0p.png)


* 修改号代码，开始服务器和客户端
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864396000mkbwuw.png)


8. 服务器端通过事件来监听收到的数据

**在`server.on`里面添加**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864629000ei8kkp.png)

> chunk 二进制文件
> toString() 将二进制文件装换为字符串

**结果**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864644000his51x.png)

9. 服务器端发送数据给客户端

**在`server.on`里面添加**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158648260005hcaz4.png)



**在`clent.on`里面添加**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864854000cokjqs.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864902000yojfpf.png)


10. 断开连接

**服务器端**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715864941000w9hlmk.png)

抓包结果

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171586525600085dw8c.png)

> 1. 服务器端向客户端发送想断开连接`FIN`,并且确定收到了断开前的数据`ACK`。
> 2. 客户端确定都到了`ACK`
> 3. 因为数据还没有发送完，客户端继续发送数据
> 4. 服务器端确定收到了发送的数据`ACK`.
> 5. 客户端发送完了数据告诉服务器可以断开连接了`FIN`
> 6. 服务器端确定收到了断开的消息`ACK`


**客户端断开连接**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715865861000fu3168.png)


11. 非正常的断开连接，监听错误

非正常断开连接，比如`ctrl+c`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715866014000qew0y4.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158660260009ghlmw.png)

有了这段代码后，服务器就不会更着客户端崩溃而崩溃了，
客户端重新启动就又可以建立连接



# 二、基于 TCP 协议的聊天室
## 2.1 聊天室的结构定义
**信息的格式**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171586652300008xxx7.png)


**格式的转换**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715866723000surgka.png)


**聊天室的功能：**

* 用户需要先输入用户名才可以进入聊天室
* 每当新用户进入聊天室时，所有用户都会收到欢迎消息
* 聊天时，其他所有用户都会收到该消息
* 每当用户离开聊天室时，其他用户都会收到该用户离开的消息

**对收发双方的一个约定**

* 这个约定就是一种协议（运用层），类似`HTTP`的这种协议，不过是自己规定的一些简单协议

**新用户进入聊天室时**

* 客户端要向服务器发送一个 JSON 的数据![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715867259000rory1a.png)

* 当服务器收到后，需要向所有的客户端广播一个消息![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715867385000784kt8.png)

**聊天时**

* 发送端时，发送端需要向服务器发送消息![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17158675180003cl713.png)
* 接受端，服务器需要向其他的客户端转发这个消息![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715867573000bqwy5u.png)

**客户离开聊天室时**

* 用户正常离开聊天室时(输入 exit)
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715867809000ac1azp.png)
* 用户非正常离开聊天室时(客户端崩溃)
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715867855000aohadf.png)


## 2.2 代码编写（后面使用node.js补全）


