# 一、什么是HTTP？
什么是HTTP呢？我们来看一下维基百科的解释： 

* 超文本传输协议（英语：HyperText Transfer Protocol，缩写：HTTP）是一种用于分布式、协作式和超媒体信息系统的应用层协议； 
* HTTP是万维网的数据通信的基础，设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法； 
* 通过HTTP或者HTTPS协议请求的资源由统一资源标识符（Uniform Resource Identifiers，URI）来标识；

HTTP是一个客户端（用户）和服务端（网站）之间请求和响应的标准。 

* 通过使用网页浏览器、网络爬虫或者其它的工具，客户端发起一个HTTP请求到服务器上指定端口（默认端口为80）； 
	* 我们称这个客户端为用户代理程序（user agent）； 
* 响应的服务器上存储着一些资源，比如HTML文件和图像。 
* 我们称这个响应服务器为源服务器（origin server）；

# 二、网页中资源的获取
我们网页中的资源通常是被放在Web资源服务器中，由浏览器自动发送HTTP请求来获取、解析、展示的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17337133980001ubw4w.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733713414000qwv5im.png)

目前我们页面中很多数据是动态展示的： 

* 比如页面中的数据展示、搜索数据、表单验证等等，也是通过在JavaScript中发送HTTP请求获取的；

# 三、HTTP的组成
一次HTTP请求主要包括：请求（Request）和响应（Response）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17337135410003mr8bl.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733713549000udl155.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733713554000o5msdy.png)

# 四、HTTP的版本
**HTTP/0.9** 
 
 * 发布于1991年； 
 * 只支持GET请求方法获取文本数据，当时主要是为了获取HTML页面内容； 
 
 **HTTP/1.0**
 
  * 发布于1996年； 
  * 支持POST、HEAD等请求方法，支持请求头、响应头等，支持更多种数据类型(不再局限于文本数据) ； 
  * 但是浏览器的每次请求都需要与服务器建立一个TCP连接，请求处理完成后立即断开TCP连接，每次建立连接增加了性能损耗；
  
  **HTTP/1.1(目前使用最广泛的版本)** 
  
  * 发布于1997年； 
  * 增加了PUT、DELETE等请求方法； 
  * 采用持久连接(Connection: keep-alive)，多个请求可以共用同一个TCP连接； 
  
**2015年，HTTP/2.0**
  
**2018年，HTTP/3.0**

# 五、HTTP的请求方式
在RFC中定义了一组请求方式，来表示要对给定资源执行的操作： 

* **GET**：GET 方法请求一个指定资源的表示形式，使用 GET 的请求应该只被用于获取数据。 
* **HEAD**：HEAD 方法请求一个与 GET 请求的响应相同的响应，但没有响应体。 
	* 比如在准备下载一个文件前，先获取文件的大小，再决定是否进行下载； 
* **POST**：POST 方法用于将实体提交到指定的资源。 
* **PUT**：PUT 方法用请求有效载荷（payload）替换目标资源的所有当前表示；
* **DELETE**：DELETE 方法删除指定的资源； 
* **PATCH**：PATCH 方法用于对资源应部分修改； 
* **CONNECT**：CONNECT 方法建立一个到目标资源标识的服务器的隧道，通常用在代理服务器，网页开发很少用到。 
* **TRACE**：TRACE 方法沿着到目标资源的路径执行一个消息环回测试。

**在开发中使用最多的是GET、POST请求；**

* 在后续的后台管理项目中，我们也会使用PATCH、DELETE请求；


# 六、HTTP Request Header
在request对象的header中也包含很多有用的信息，客户端会默认传递过来一些信息：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733714271000wopyvg.png)

**content-type是这次请求携带的数据的类型：** 

* **application/x-www-form-urlencoded**：表示数据被编码成以 '&' 分隔的键 - 值对，同时以 '=' 分隔键和值 
* **application/json**：表示是一个json类型； 
* **text/plain**：表示是文本类型； 
* **application/xml**：表示是xml类型； 
* **multipart/form-data**：表示是上传文件；

**content-length**：文件的大小长度 

**keep-alive：** 

* http是基于TCP协议的，但是通常在进行一次请求和响应结束后会立刻中断；
* 在http1.0中，如果想要继续保持连接： 
	* 浏览器需要在请求头中添加 connection: keep-alive； 
	* 服务器需要在响应头中添加 connection:keep-alive； 
	* 当客户端再次放请求时，就会使用同一个连接，直接一方中断连接； 
* 在http1.1中，所有连接默认是 connection: keep-alive的；
* 不同的Web服务器会有不同的保持 keep-alive的时间；
* Node中默认是5s中；

**accept-encoding**：告知服务器，客户端支持的文件压缩格式，比如js文件可以使用gzip编码，对应 .gz文件； 

**accept**：告知服务器，客户端可接受文件的格式类型； 

**user-agent**：客户端相关的信息；

# 七、HTTP Response响应状态码
Http状态码（Http Status Code）是用来表示Http响应状态的数字代码： 

* Http状态码非常多，可以根据不同的情况，给客户端返回不同的状态码； 
* MDN响应码解析地址:https://developer.mozilla.org/zh-CN/docs/web/http/status

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733715175000960fsg.png)

> 大于400都是错误的请求

# 七、HTTP Response Header
响应的header中包括一些服务器给客户端的信息：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733715442000lx07xs.png)


# 八、Chrome安装插件 - FeHelper
为了之后查看数据更加的便捷、优雅，我们安装一个Chrome插件：

* 方式一：可以直接通过Chrome的扩展商店安装；
* 方式二：手动安装 ， 下载地址:https://github.com/zxlie/FeHelper/tree/master/apps/static/screenshot/crx

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733715750000rmh7hv.png)


