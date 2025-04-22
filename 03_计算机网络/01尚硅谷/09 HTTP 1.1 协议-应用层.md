# 一、认识 HTTP 协议
**超文本传输协议 Hyper Text Tansfer Protoco**

**最初目的:提供一种发送和接 HTML 页面的方法**

**版本:HTTP/0.9、HTTP/1.0.HTTP/1.1、HTTP/2、HTTP/3**
* 低版本向前兼容

* HTTP 是基于 TCP 协议的应用层协议

* HTTP 是一个**请求-响应协议**

* 客户端发送请求，服务器端接收请求，处理后给出响应

* **发送请求前需要先建立 TCP 连接**

**HTTP 的通信过程**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715928730000yvlxom.png)

**抓包结果：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715928998000wog10p.png)

# 二、HTTP 报文格式
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715929243000tmm2s6.png)

* 使用 HTTP 协议需要遵守 HTTP 协议的报文格式
* HTTP 报文分为请求报文和响应报文
* 请求报文和响应报文分别有自己的格式

**HTTP 的协议首部采用 ASCI 编码**

**抓包原本的样子：**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715929397000f92gxo.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17159293250000is8l6.png)

**红色为 HTTP 请求报文，紫色为相应报文**

## 2.1 HTTP 请求报文
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715930061000o059lw.png)

**首部行并没有规定个数**

**URL 表示路径 `/` 根路径**

## 2.2 HTTP 响应报文
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715930187000zjqgnu.png)


# 三、RESTfuI 风格的 API

就是一种 API的设计风格，不是强制约定

APl, Application Programning Interface，应用编程接口

的接口这里指客户端和服务器端通信

客户端使用指定的 HTTP 方法请求指定的 URL，完成与服务器的交互

## 3.1 什么是 RESTful
RESTful是一种架构风格，基于HTTP协议，旨在简化网络架构、降低耦合度、提高可扩展性和可读性。RESTful架构通常使用资源（Resource）来描述服务器上的一些实体，每个资源都对应一个唯一的URI，客户端可以通过HTTP方法（GET、POST、PUT、DELETE等）来操作这些资源。RESTful架构的优点包括：

- 简化了架构，降低了耦合度
- 提高了可扩展性和可读性
- 便于客户端和服务器的解耦
- 支持缓存和负载均衡

RESTful架构的六个架构约束包括：

- 客户端-服务器架构
- 无状态架构
- 可缓存架构
- 统一接口架构
- 分层架构
- 按需编码架构

RESTful架构广泛应用于Web服务和移动应用开发中，例如Google Maps、Twitter API等。

## 3.2 什么是 API
API（Application Programming Interface，应用程序接口）是一种允许不同的软件系统之间相互通信和交互的接口。API通常定义了一组规则和协议，用于访问和操作某个应用程序或系统的数据和功能。

API的主要作用是：

- 提供了一个抽象层，隐藏了底层实现细节
- 允许不同的系统和语言之间进行交互和集成
- 提高了开发效率和灵活性
- 降低了系统之间的耦合度

常见的API类型包括：

- Web API：用于Web应用程序之间的交互，通常使用HTTP协议
- Operating system API：用于操作系统和应用程序之间的交互，例如Windows API和Linux API
- Library API：用于软件库和应用程序之间的交互，例如Java API和Python API

API的设计原则包括：

- 简洁性
- 一致性
- 灵活性
- 可扩展性
- 安全性

API的安全性非常重要，需要考虑身份验证、授权、加密和输入验证等问题，以防止攻击和数据泄露。

## 3.2 API 的分类
**一般风格的 API**

* GET localhost:3000/getUsers 获取全部用户信息
* GET localhost:3000/getUser?id=1 获取指定用户信息
* POST localhost:3000/addUser 创建新用户
* POST localhost:3000/deleteUser?id=1 删除指定用户
* POST localhost:3000/updateUser?id=1 修改指定用户

**RESTful风格的 API会配合各种请求方法，使 API设计的更优雅**

**RESTful风格的 API**

* GET localhost:9000/users 获取全部用户信息
* GET localhost:9000/users/1 获取指定用户信息
* POST localhost:9000/users 创建新用户
* DELETE localhost:9000/users/1 删除指定用户
* PATCH localhost:9000/users/1 修改局部指定用户


# 四、URL
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716024027000d9s3nq.png)


**URI、URL和 URN**

* URI是一个用来标识资源的字符串
* URI分为定位符(URL)和名字(URN)
* URL除了确定一个资源，还提供一种定位该资源的机制
* URN 就是一个特殊的名字，指的是资源而不指定其位置

**URL:**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716024410000bawbfa.png)


`user:pass：`现在都是省略的，有缓存，为了安全

`port：`端口号，是可以省略的

`path：`路径

`#hash：`表示在客户端的那个位置

**URN:**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716024474000bj960a.png)


## 4.1 RUL 编码
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716024548000b7334v.png)

**URL 本身使用 ASCII 编码**

**URL 中出现 ASCI 字符集之外的字符，比如中文时，需要进行 URL 编码**

* 先对中文进行 UTF-8 编码，再在每个字节前加 % 字符前缀
* 比如“你”的 UTF-8 编码是 e4bda0，URL 编码后变为 %e4%bd%a0
* 再对 %e4%bd%a0 进行 ASCII 编码，得到最终的二进制形式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716024778000zbkvnf.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716024867000f9x2w9.png)

**还需要对可能造成歧义的字符进行编码，比如query中的 =、&、#、% 等**
* 先对它们进行 ASCII 编码，再在每个字节前加 % 字符前缀
* 比如“&”的 ASCII 编码是 26，URL 编码后变为 %26
* 再对 %26 进行 ASCII 编码，才得到最终的二进制形式 0x253236

**使用浏览器发送请求时，浏览器已经对非 ASCI 字符做过 URL 编码了**


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17160253900003sasvl.png)

# 五、 HTTP 响应状态码
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716093032000iaba4f.png)


**表明 HTTP 请求是否成功完成，分为五类**

* 100~199 信息响应:请求已收到，请继续
* 200~299 成功响应:请求成功
* 300~399 重定向响应:为了完成请求还有其它操作要做>
* 400~499 客户端错误响应:请求包含错误的语法或无法被处理
* 500~599 服务端错误响应:服务器无法处理请求

## 5.1 1xx
**信息响应:请求已收到，请继续**

* 100 Continue（继续）迄今为止请求的所有内容都是可行的，客户端应该继续请求。如果已经完成，则忽略它
* 101 Switching（转接） Protocols 响应客户端的 Upgrade 首部字段，指明服务器即将切换的协议

## 5.2 2xx
**成功响应:请求成功**

* 200 OK  请求成功
* 206 Partial Content  当客户端请求资源的一部分时，将使用此状态码表示响应的是资源的一部分


## 5.3 3xx
**重定向响应:为了完成请求还有其它操作要做**

* 301 Moved Permanently 请求资源的 URL 已永久更改。会在响应中通过 Location 头字段给出要跳转的 URL，该URL 会被客户端持久缓存![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716095979000xcw96g.png)

* 302 Found 请求资源的 URL暂时更改。会在响应中通过Location 头字段给出要跳转的 URL，该URL 一般不会被客户端持久缓存
* 304 Not Modified 用于缓存。告诉客户端响应还没有被修改，因此客户端可以继续使用缓存的内容

## 5.4 4xx
**客户端错误响应:请求包含错误的语法或无法被处理**

* 400 Bad Request  由于客户端错误(例如错误的请求语法)，服务器无法或不会处理请求
* 401 Unauthorized  当前请求需要身份验证
* 403 Forbidden  客户端没有访问内容的权限，因此服务器拒绝提供请求的资源
* 404 Not Found  服务器找不到请求的资源
* 405 Method Not Allowed  目标资源不支持该方法。例如，不允许使用POST 来获取资源


## 5.5 5xx
**服务端错误响应:服务器无法处理请求**

* 500 Internal Server Error  服务器遇到了不知道如何处理的情况
* 501 Not lmplemented  服务器无法处理该请求方法。服务器至少能够处理的唯二方法(因此不能返回此代码)是GET 和 HEAD
* 502 Bad Gateway  作为网关或代理服务器从上游服务器得到的响应是一个错误的响应
* 503 Service Unavailable  服务器没有准备好处理请求。常见原因是请求过多导致服务器太忙或正在维护中
* 504 Gateway Timeout  网关还在，但后端服务因为各种原因(比如因为一个死循环卡死了)，导致一直没有响应回来，过了一段时间后网关依旧没能收到消息，就会给客户端返回 504 网关超时

## 5.6 小结
**表明 HTTP 请求是否成功完成，分为五类**

* 100~199 信息响应:请求已收到，请继续
* 200~299 成功响应:请求成功
* 300~399 重定向响应:为了完成请求还有其它操作要做做
* 400~499 客户端错误响应:请求包含错误的语法或无法被处理
* 500~599 服务端错误响应:服务器无法处理请求


# 六、代理服务器和VPN
## 6.1 代理服务器
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716101483000sxxtpu.png)


处于客户端和目标服务器之间，转发上下游的请求和响应

**分为正向代理和反向代理的定义**

* 正向代理代理的对象是客户端

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716101543000h7ee6k.png)




* 反向代理代理的对象是服务端

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716101565000u17j77.png)



**分为正向代理和反向代理的作用：**

* 正向代理的作用:突破访问限制、隐藏客户端身份、过滤内容等
* 反向代理的作用:负载均衡、隐藏服务器身份等

**设置代理服务器：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716102103000tmyp1d.png)

## 6.2 VPN
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716102209000vgtg8v.png)

虚拟私人网络 Virtual Private Network

在公共网络上建立专用网络，加密通信

因为是加密通信，其他人无法知道通信内容

一般需要专门的 VPN 软件来完成通信

**VPN 的作用：**

* 提高上网安全
* 隐藏用户身份
* 突破访问限制


## 6.3 代理服务器和 VPN 对比
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171610232600085mopo.png)

# 七、首部字段
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716104984000yyp7hh.png)

客户端和服务器之间可以通过首部字段传递附加信息

可以分为请求首部字段、响应首部字段、通用首部字段

**请求首部字段：**

* 客户端向服务器发送请求报文时使用的首部字段
* 附加了请求的额外信息:客户端身份信息、期待获取的资源信息等

**响应首部字段：**

* 服务器向客户端返回响应报文时使用的首部字段
* 附加了响应的额外信息:服务器的身份信息、客户端该如何处理内容等


## Host
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716105338000j8k21p.png)

HTTP/1.1 引入了虚拟主机的概念，使得多个域名可以共享同一个IP地址

即同一个 Web 服务器上可以搭建多个网站，共用同一个公网 IP

客户端发送请求时，需要通过 Host 字段明确指定请求的目标站点

服务器通过 Host 字段才能正确地处理请求

## Referer
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17161026230002s085e.png)

通常被网站用来统计用户来源

也可以用来防盗链

## Location
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716102691000qdy20q.png)

一般配合 HTTP 状态码 301 或 302 使用

## Content-Disposition
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171610275900069qs1a.png)

inline 默认值，响应内容作为页面的一部分展示

`attachment; filename="ascii.png"`，响应内容以附件的形式下载

在`multipart/form-data` 中，用来给出其对应字段的相关信息

## Allow
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716102983000p5vdjm.png)


若服务器返回状态码 405 Method Not Allowed

则需要通过 Alow 首部字段告诉客户端可以使用什么请求方法

## User-Agent
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716103051000a506mv.png)

可以用来统计访问网站的客户端

可以判断发送请求的是 PC 端还是移动端，从而响应不同的内容

## 连接管理
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716103930000clupdy.png)


HTTP/1.1规定所有连接都必须是持久(长)的

持久(长)连接可以避开三次握手和 TCP 慢启动的拥塞适应阶段

Keep-Alive 字段需要 Connection: keep-alive 才有意义

timeout: 空闲连接需要保持打开状态的最小时长(单位:秒)

max: 在连接关闭之前，此连接可以发送的请求的最大值

## Content-Length
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716106148000qb6onh.png)

Content-Length 必须准确描述主体内容的字节长度，不能多不能少

接收方会根据 Content-Length 来接收指定长度的数据

只有能确定主体的全部长度，才可以使用 Content-Length

如果无法确定主体的全部长度，可以使用 Transfer-Encoding:chunked

## Transfer-Encoding:chunked
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17161064140002gg3t1.png)

chunked 表明主体内容以一系列分块编码的形式进行发送

此时不能确定主体的全部长度

如果无法确定主体的全部长度，可以使用 Transfer-Encoding:chunked

如果能确定主体的全部长度，可以使用 Content-Length

**分块响应数据格式如图所示**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171610653800085z5b5.png)

* 数字是 16 进制，表示字节数
* Content-Length:2 中的数字是 10 进制

## Accept-内容协商
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17161067660001p1sis.png)


## 响应 Content-Type
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716106958000oggdol.png)


服务器可以从 Accept 中选一个，使用 Content-Type 告诉客户端

同时还可以告诉客户端使用什么字符编码

客户端可以根据响应中的 Content-Type 决定如何处理获取的响应主体

## 请求 Content-Type
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716107380000q1n9pr.png)

一般用于指明请求体携带的数据是什么格式

服务器可以根据此字段，采取对应措施处理请求数据

常用类型还有:`application/json`和`multipart/form-data`
 
## 媒体类型
格式:type/subtype(text/html、text/css、application/javascript)

type: text/image/audio/vedio/application/multipart/message 等

大小写不敏感，通常使用小写

媒体类型查询：https://www.iana.org/assignments/media-types/media-types.xhtm

## 内容压缩
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716109164000ouw37w.png)

通常用于对实体内容进行压缩编码，目的是减小文件大小，优化传输

服务器压缩文本文件后再传输，客户端收到压缩后的文件再解压缩

> 图片本事就是进行过压缩了的，一般不会在进行压缩

## HTTP 首部字段小结
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17161094850005xtu0b.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716109561000asqxnw.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716109614000g7rjaj.png)

# 八、文件上传

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17161097140006i5qgl.png)

**文件上传的原理：**

* 上传文件需要使用 multipart/form-data 格式的数据
* 客户端需要通过 Content-Type 告诉服务器使用的数据格式
* 服务器从 multipart/form-data 格式的数据中拿到文件保存到服务器的磁盘上

**form-data 格式的读取：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716109945000qxuwsa.png)

* multipart - 多部分

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716294057000oqhxm7.png)

Content-Type:multipart/form-data; boundary=xxx（客户端添加的）

服务器从请求的 Content-Type 中拿到 boundary

根据 form-data 的格式一行行解析

解析出来的参数保存到对象中，文件保存到磁盘上


# 九、断点续传
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716294397000njaapp.png)

**断点续传原理：**

* 客户端需要记住目前数据传输到哪个字节了
* 客户端通过首部字段告诉服务器响应 start-end 字节范围内的数据
* 服务器接收到请求后读出相应的首部字段
* 服务器按照请求的要求响应指定字节范围内的数据

# 十、视频播放
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17162946910005eb0iq.png)

**视频播放原理**

* 播放视频时，需要边看边请求，而不是一次加载整个视频资源
* 客户端不断通过 Range 字段告诉服务器响应 start-end 范围内的数据
* 服务器接收到请求后读出 Range 字段的值
* 服务器按照请求的要求不断响应指定字节范围内的数据

# 十一、单向散列函数

也称为消息摘要(Message Digest)函数、哈希(Hash)函数

函数的输出称为散列值、消息摘要、指纹

可以根据消息内容计算出散列值

内容即使只发生了1位的改变，也会生成完全不同的散列值

可以通过散列值来判断文件内容是否发生了改变

单向的意思是:方向不可逆无法从散列值还原出原始内容

常见的单向散列函数有 MD5、SHA-1、SHA-256等

户密码单向散列函数还可用于加密用
* 使用散列函数加密密码
* 密码明文存储很危险，很多用户在各个网站的账号和密码都是一样的，一个网站的数据库泄露，就会导致很严重的后果
* 用户注册时输入密码 123456，经过加密后保存到数据库中
* 用户登录时输入密码 123456，经过加密后和数据库中的密码比对

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716295607000taw5z4.png)


出原始密码，但可以暴力破解一部分无法直接从加密后的密码还原

* 通过代码大量生成散列值，将原始数据和散列值保存到数据库中 1->xxx 2->yyy 3->zZz 123456->aaa
* 想要破解时，通过散列值去数据库中查询，查到了就破解成功，查不到就破解失败

# 十二、HTTP 缓存
**没有缓存的时候：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17162963160009ta3iu.png)

**有缓存的时候：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716296385000j3ihfq.png)


**HTTP 缓存原理：**

* HTTP 缓存是通过相关首部字段在服务器和客户端之间的一种约定
* 客户端向服务器请求资源，服务器响应资源给客户端
* 同时，服务器通过相关首部字段告诉客户端是否缓存该资源以及如何缓存
* 客户端按照服务器的要求将资源保存在内存或硬盘中(或不缓存)
* 再请求相同路径时，先查找缓存，存在并未过期则直接使用本地缓存

一般只有静态资源会被缓存，比如：CSS、JS等

**HTTP 的缓存情况：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716296799000ehebjd.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716296948000knm6in.png)

**半段资源是否被修改：**

* 缓存前后的 ETag 和 Last-Modified 是否被修改过

**HTTP 的首部字段：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716297127000ba7uo8.png)

* 在 HTTP 中，时间都是用格林尼治标准时间来表示的，而不是本地时间
* 可以用于计算缓存的内容是否已过期
	* Date - 缓存的时间 > 0 侧没有过期，反之过期

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716297266000kmnu1f.png)

* public 和 private 只可以有一个
* public 和 private 可以和后面的联合使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716297531000i889wu.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716297581000vpui6t.png)

* Last-Modified 只能精确到秒，有些资源更新很快，这个时候就产生了 ETag 

**ETag：**

* 资源本质上就是二进制0和1
* 可以使用单向散列函数根据这些 0和1计算出散列值
* 如果资源不变化，每次计算出的这个值就不变
* 如果资源发生变化，哪怕只是一位的微小变化，计算出的这个值也会改变
* 我们可以通过这个值来判断资源是否发生了修改

如果资源过大，不方便计算资源内容的散列值

还可以用资源修改时间和大小的散列值代替内容的散列值

HTTP 没有明确指定生成 ETag 值的方法，可以根据需要使用合适的方法

**ETag 和 Last-Modified：**

优先使用 ETag 来判断资源是否修改

ETag 不存在才使用 Last-Modified 来判断资源是否修改

Last-Modified 不仅仅对缓存有用，也可用来显示上次修改时间

最好同时提供 ETag 和 Last-Modified


客户端缓存失效前，如果文件发生了变化，如何主动让缓存失效?
不缓存 HTML，通过添加 query 参数的方式改变 HTML 中请求的 URL

**小结：**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716298513000yidx55.png)


# 十三、CDN
内容分发网络 Content Delivery Network

指的是一组分布在各地的服务器，这些服务器存储着数据的副本

请求时，选择距离近、负载轻的缓存服务器，更快地将资源响应给用户

广泛用于传输 CSS、JavaScript、图片等静态资源

内容所有者向 CDN 运营商支付费用，CDN将内容分发给用户

**CDN 原理：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716298771000t5u3jp.png)


**CDN 的好处：**

 * 可以减轻我们自身服务器的请求压力
* CDN 的服务器在地理位置上可能比自己的服务器更接近用户，速度更快
* CDN 已经做了恰当的缓存设置，不需要我们再配置了

**CDN 抓包：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17162991940007kco5b.png)


# 十四、动态资源和静态资源
**静态资源：**

* 静态资源是不怎么变化的资源，无论是谁访问，都会得到相同的结果
* js、css、没有动态内容的 html、图片等都是静态资源
* 静态资源需要缓存(一般 HTML不缓存)，也有必要缓存
* 静态资源可以使用CDN

**动态资源：**

* 动态资源不是固定不变的，一般会根据数据库中的数据动态变化
* 有动态内容的 HTML 文件是动态资源
* 动态资源一般不需要缓存
* 动态资源一般不使用CDN

# 十五、前后端分离
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716881225000jct1d1.png)


**前后端未分离：**

* 前端开发 HTML、CSS、JS 等静态内容
* 后端开发动态内容，并在 HTML 文件中嵌入模板
* 直接请求就能拿到完整页面(服务器返回的就是完整页面)
* 缺点:前后端需要一起部署:无法使用 CDN:前后端代码混杂在一起
* 优点:利于 SEO 优化
	* SEO优化（Search Engine Optimization）是指通过了解搜索引擎的运作规则和算法，针对网站或网页的内容、结构和编码等方面进行优化，以提高网站在搜索引擎中的排名和可见性，从而提高网站的访问量和转换率。

**前后端部分分离：**

* 前端开发 HTML、CSS、JS 等静态内容，(除 HTML 外)部署到静态服务器
* 后端开发动态内容，并在 HTML 文件中嵌入模板
* 直接请求就能拿到完整页面(服务器返回的就是完整页面)
* 缺点:前后端代码混杂在一起
* 优点:利于 SEO 优化，可以使用 CDN;没有跨域问题


**前后端完全分离：**

* 前端开发 HTML、CSS、JS 等静态内容，部署到静态资源服务器上
* 后端开发接口，部署到其他服务器上，前后端分开部署
* 前端通过 JavaScript 访问后端提供的接口获取数据，再渲染到页面上
* 优点:前后端可以分开部署;可以使用 CDN:代码不再混杂在一起
* 缺点:不利于 SEO 优化;存在跨域问题


# 十六、跨域
协议、域名或端口号有一个不同，就是不同域，不同域之间就是跨域
* `http://www.imooc.com` 和` https://www.imooc.com `就是不同域
* `http://www.imooc.com/course` 和`http://www.imooc.com/list `是同域

浏览器出于安全考虑，限制脚本内发起的跨域 HTTP 请求

跨域问题和服务器没关系，跨域响应可以到达浏览器，但是被浏览器阻止

浏览器默认不允许跨域，但有时跨域又是必须的
 
## 16.1 CORS 
使用 CORS 可以使浏览器允许跨域

CORS(Cross-Origin Resource Sharing，跨域资源共享)

CORS 基于特定的 HTTP 头，浏览器识别到这些头，决定是否允许跨域

针对简单请求和预检请求跨域，需要使用不同的 CORS 头字段

**简单请求：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716380779000majz6u.png)

**预检请求：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17163808750005xklh4.png)


## 16.2 跨域获取数据-简单跨域请求

**不应许跨域：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171638099400093cua8.png)

**应许跨域：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716381036000sujfjd.png)

**使用 POST 方法：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17163811450006onnye.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716381303000xzhdf5.png)


## 16.3 跨域发送数据-预检跨域请求

不满足简单请求的条件

实际请求前，发送预检请求

获知服务器是否允许实际请求

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17163814800004ityzp.png)

不应许和上面一样只发送一个 HTTP 响应

## 16.4 代理服务器
也可以使用代理服务器解决跨域问题

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716381548000fhnrtn.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716381563000ai6bos.png)




