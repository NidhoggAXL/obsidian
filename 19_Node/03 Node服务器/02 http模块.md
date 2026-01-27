# 一、Web服务器

什么是Web服务器？

 - 当应用程序（客户端）需要某一个资源时，可以向一台服务器，通过Http请求获取到这个资源；
 - 提供资源的这个服务器，就是一个Web服务器；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17660667030003oje2q.png)

目前有很多开源的Web服务器：Nginx、Apache（静态）、Apache Tomcat（静态、动态）、Node.js

# 二、http模块

在Node中，提供web服务器的资源返回给浏览器，主要是通过http模块。

先简单对它做一个使用：

```js
import http from 'http'

// 创建服务器
const server = http.createServer((request, response) => {
  response.end('hello world')//通过end来关闭服务器
})

// 开启服务器
server.listen(3000, () => {
  console.log('3000 端口服务器启动成功')
})
```

# 三、创建服务器

创建服务器对象，我们是通过 createServer 来完成的

 - http.createServer会返回服务器的对象；
 - 底层其实使用直接 new Server 对象。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176611275600035lxcl.png)

那么，当然，我们也可以自己来创建这个对象：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176611276700046ramk.png)

上面我们已经看到，创建Server时传入一个回调函数，这个回调函数在
被调用时会传入两个参数：

 - **req**：request请求对象，包含请求关的信息；
 - **res**：response响应对象，包含我要发送给客户端的信息；

# 四、监听主机和端口号

<mark class="hltr-cyan">Server通过listen方法来开启服务器</mark>，并且在某一个主机和端口上监听网络请求：

 - 也就是当我们通过 ip:port 的方式发送到我们监听的Web服务器上时；
 - 我们就可以对其进行相关的处理；

listen函数有三个参数：

 - **端口port**: 可以不传, 系统会默认分配端, 后续项目中我们会写入到环境变量中；
 - **主机host**: 通常可以传入localhost、ip地址127.0.0.1、或者ip地址0.0.0.0，默认是0.0.0.0；
	 - localhost：本质上是一个域名，通常情况下会被解析成127.0.0.1；
	 - 127.0.0.1：回环地址（Loop Back Address），表达的意思其实是我们主机自己发出去的包，直接被自己接收；
		 - 正常的数据库包经常 应用层 - 传输层 - 网络层 - 数据链路层 - 物理层 ；
		 - 而回环地址，是在网络层直接就被获取到了，是不会经常数据链路层和物理层的；
		 - 比如我们监听 127.0.0.1时，在同一个网段下的主机中，通过ip地址是不能访问的；
 - **0.0.0.0**：
	 - 监听IPV4上所有的地址，再根据端口找到不同的应用程序；
	 - 比如我们监听 0.0.0.0时，在同一个网段下的主机中，通过ip地址是可以访问的；

 - **回调函数**：服务器启动成功时的回调函数；

# 五、补充

## 5.1 PostMan

因为浏览器里面，只能通过 url 地址，手动的发送 GET 请求，无法进行其他的网络请求，以及对 header 的配置，所有下载 PostMan 的专业工具来进行网络请求。

https://postman.xiniushu.com/

## 5.2 nodemon

我们修改了启动 http 服务的node程序的时候，默认是不会关闭的，当我们修改了代码内容，那么就需要在终端中关闭node程序，并重新启动，这是一个麻烦的过程，可以通过一个 nodemon 的库来实现，当代码发生改变的时候，自动关闭node程序，并重新启动。

nodemon 是 node + monitor 的缩写，monitor是监听、侦测的意思：

```bash
npm install nodemon -g
```

前面都是通过 node 来启动服务，后面就可以通过 nodemon 来启动：

```bash
nodemon 启动的文件
```

当文件修改时，会自动重启node服务：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766121627000qktu8b.png)


## 5.3 多次打印

```js
import http from "http";

//创建服务器
const server = http.createServer((request, response) => {
  console.log("服务器被开启 - 请求路径:", request.url, "方法:", request.method);
  response.end("hello world");
});

// 开启服务器
server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});

```

上面的代码，如果我们是在 浏览器 里面使用 URL 的 8000 端口进行访问的话会得到下面的结果：

```text
服务器被开启 - 请求路径: / 方法: GET
服务器被开启 - 请求路径: /.well-known/appspecific/com.chrome.devtools.json 方法: GET
服务器被开启 - 请求路径: /favicon.ico 方法: GET
```

1. 主要请求：浏览器会发送对 / 的GET请求来获取页面内容

2. favicon.ico 请求：浏览器会自动尝试请求 /favicon.ico 来获取网站图标

3. 可能的额外请求：有些浏览器可能还会发送其他请求，比如：
	 - 预连接请求
	 - 某些浏览器的额外探测请求
	 - 如果使用了开发者工具，可能会有额外的网络请求

> [!tip] 如何解决这个问题？
> 使用 PostMan 来发送请求，就不会存在 浏览器 的影响
> `服务器被开启 - 请求路径: / 方法: GET`

# 五、request对象

在向服务器发送请求时，我们会携带很多信息，比如：

 - 本次**请求的URL**，服务器需要根据不同的URL进行不同的处理；
 - 本次**请求的请求方式**，比如GET、POST请求传入的参数和处理的方式是不同的；
 - 本次**请求的headers中也会携带一些信息**，比如客户端信息、接受数据的格式、支持的编码格式等；
 - 等等...

这些信息，Node会帮助我们封装到一个**request的对象中**，我们可以直接来处理这个request对象：

```js
import http from 'http'

const server = http.createServer((request, response) => {
  console.log(request.url)// /
  console.log(request.method)// GET
  console.log(request.headers)
  // 请求头
  // {
  //   'user-agent': 'PostmanRuntime/7.51.0',
  //   accept: '*/*',
  //   'postman-token': '0a2529ef-b971-4f3f-ba9e-a11e792b9b4d',
  //   host: 'localhost:3000',
  //   'accept-encoding': 'gzip, deflate, br',
  //   connection: 'keep-alive'
  // }
  response.end('hello world')
})

// 开启服务器
server.listen(3000, () => {
  console.log('3000 端口服务器启动成功')
})
```

## 5.1 URL的处理

客户端在发送请求时，会请求不同的数据，那么会传入不同的请求地址：

 - 比如 http://localhost:8000/login
 - 比如 http://localhost:8000/products

服务器端需要根据不同的请求地址，作出不同的响应：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766121175000ellwwv.png)

## 5.2 URL的解析

那么如果用户发送的地址中还携带一些额外的参数呢？

 - http://localhost:8000/login?name=axl&password=123
 - 这个时候，url的值是 `/login?name=why&password=123`

```js
import http from "http";
import url from 'url'
import qs from 'querystring'

//开启服务器
const server = http.createServer((request, response) => {
  // 请求的url解析
  const urlString = request.url
  console.log(urlString)///login?name=axl&password=123

  // 请求的url路径信息解析
  const { pathname, query} = url.parse(request.url);
  console.log("请求路径名=>", pathname)//请求路径名=> /login
  console.log("请求参数=>", query)//请求参数=> name=axl&password=123

  // 请求的 GET 参数解析
  const params = qs.parse(query)
  console.log("请求参数对象=>", params)
  //请求参数对象=> { name: 'axl', password: '123' }

  // 上面 GET 参数的解析，可以使用 URLSearchParams,是一个更加标准的 API,通用性更强
  // const params = new URLSearchParams(query)
  // console.log("请求参数对象=>", params)
  //请求参数对象=> URLSearchParams { 'name' => 'axl', 'password' => '123' }

  response.end("hello world");
});

server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});

```

> [!tip] node中对 qs 的说明：
> `querystring` 的性能优于 `URLSearchParams`，但它并非标准化 API。当性能要求不高或需要与浏览器代码兼容时，请使用 `URLSearchParams`。
> 

## 5.3 method

在Restful规范（设计风格）中，我们对于数据的增删改查应该通过不同的请求方式：

 - GET：查询数据；
 - POST：新建数据；
 - PATCH：更新数据；
 - DELETE：删除数据；

所以，我们可以通过判断不同的请求方式进行不同的处理。

 - 比如创建一个用户：
 - 请求接口为 /users；
 - 请求方式为 POST 请求；
 - 携带数据 username 和 password（POST请求的数据需要放到请求体中的 body 中）；

### 创建用户接口

请求方式 ：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766124854000tmc3yq.png)


> [!tip]
> 一定要知道 <mark class="hltr-cyan">request 的本质是一个可读流</mark>，那么就可以使用可读流上面的方法。

我们程序中如何进行判断以及获取对应的数据呢？

 - 这里我们需要判断接口是 /users，并且请求方式是POST方法去获取传入的数据；
 - 获取这种body携带的数据，我们需要通过**监听 request 的 data事 件来获取**；
****
```js
import http from "http";

const server = http.createServer((request, response) => {
  // 设置 request 的编码方式
  request.setEncoding("utf-8");

  // 记录登录状态
  let isLogin = false;

  request.on("data", (data) => {
    // console.log(data)// 获取到的是一个 JSON 的字符串
    const loginInfo = JSON.parse(data)
    // console.log(loginInfo)//{ name: 'axl', password: '123' }
    if (loginInfo.name === "axl" && loginInfo.password === "123") {
      isLogin = true
    } else {
      isLogin = false
    }
  })

  request.on("end", () => {
    if (isLogin) {
      console.log("登录成功，欢迎回来~")
    } else {
      console.log("帐号或者密码错误，请重新输入===》")
    }
  })

  response.end("请求成功");
});

// 开启服务器
server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});

```

> [!node] 将JSON字符串格式转成对象类型，通过 [[01 JSO（非常重要）#4.4 parse方法|JSON.parse]] 方法即可。

## 5.4 Request Header

request对象的header中也包含很多有用的信息，客户端会默认传递过来一些信息：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766125202000k1ax0b.png)

<mark class="hltr-cyan">content-type是这次请求携带的数据的类型：</mark>

 - **application/x-www-form-urlencoded**：表示数据被编码成以 '&' 分隔的键 - 值对，同时以 '=' 分隔键和值
 - **application/json**：表示是一个json类型；
 - **text/plain**：表示是文本类型；
 - **application/xml**：表示是xml类型；
 - **multipart/form-data**：表示是上传文件；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766125267000a05a8a.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176612528300086gpxa.png)

<mark class="hltr-cyan">content-length</mark>：文件的大小长度

<mark class="hltr-cyan">keep-alive</mark>：

 - http是基于TCP协议的，但是通常在进行一次请求和响应结束后会立刻中断；
 - 在http1.0中，如果想要继续保持连接：
	 - 浏览器需要在请求头中添加 connection: keep-alive；
	 - 服务器需要在响应头中添加 connection:keey-alive；
	 - 当客户端再次放请求时，就会使用同一个连接，直接一方中断连接；
 - 在http1.1中，所有**连接默认是 connection: keep-alive的**；
	 - 不同的Web服务器会有不同的保持 keep-alive的时间；
	 - **Node中默认是5s中**；

<mark class="hltr-cyan">accept-encoding</mark>：告知服务器，客户端支持的文件压缩格式，比如js文件可以使用gzip编码，对应 .gz文件；

<mark class="hltr-cyan">accept</mark>：告知服务器，客户端可接受文件的格式类型；

<mark class="hltr-cyan">user-agent</mark>：客户端相关的信息；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766125411000vn3mlo.png)

<mark class="hltr-cyan">token的携带</mark>：

| authoriaztion | bearer |
| ------------- | ------ |
| 授权            | 持有人    |


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766125475000b5706a.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766125509000ylqobv.png)

```js
import http from "http";

//开启服务器
const server = http.createServer((request, response) => {
  const token = request.headers["authorization"]
  console.log(token)//Bearer aaaaaa
  response.end("hello world");
});

server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});

```

# 六、response对象

## 6.1 返回响应结果

如果我们希望给客户端响应的结果数据，可以通过两种方式：

 - Write方法：这种方式是直接写出数据，但是并没有关闭流；
 - end方法：这种方式是写出最后的数据，并且写出后会关闭流；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17661266800002s89dh.png)

如果我们没有调用 end，客户端将会一直等待结果： 所以客户端在发送网络请求时，**都会设置超时时间**。

## 6.2 返回状态码

Http状态码（Http Status Code）是用来表示Http响应状态的数字代码：

 - Http状态码非常多，可以根据不同的情况，给客户端返回不同的状态码；
 - MDN响应码解析地址：https://developer.mozilla.org/zh-CN/docs/web/http/status

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17661267560000le8jn.png)

```js
import http from "http";

//开启服务器
const server = http.createServer((request, response) => {
  response.statusCode = 400
  response.end("hello world");
});

server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766126918000le6a3d.png)


## 6.3 响应头文件

返回头部信息，主要有两种方式：

 - res.setHeader：一次写入一个头部信息；
 - res.writeHead：同时写入header和status；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766134069000k102x5.png)

Header设置 Content-Type有什么作用呢？

- 默认客户端接收到的是字符串，客户端会按照自己默认的方式进行处理；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17661340990000zrudp.png)

# 七、http请求

**axios框架**:客户端(浏览器)和服务器(Node)

 - axios在浏览器中
	* XHR:xmlhttprequest
	* fetch
- axios在Node中
	- 不可能存在xhr/fetch(浏览器)
	* http模块

> [!tip] axios在服务器中使用的本质是使用 node 的 http 模块。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766143101000n5zqdp.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766143105000kaunyf.png)

> [!node] 上面使用的是 http 的请求，如何使用 axios 看前面的笔记就好
> 
# 八、文件上传(了解)

> [!tip]
> 在实际开发中，并不会使用下面的上传方式，而是使用一些库来进行，但是这些库的底层都是使用类似下面这种原生的方法，**可以对下面的进行一个了解**

文件上传一般都是通过 POST 请求的，并且基本都是通过表单的方式进行文件的上传，看一下 PostMan 截图：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766143931000t54ch9.png)

## 8.1 上传的基本流程

基本上传数据的过程（**这是一个错误的编码，不能写入正确的数据，只是对这个流程的简述**）：

1. 开启 node 的 http 服务，并存储文件

```js
import http from "http";
import fs from 'fs'

const server = http.createServer((request, response) => {
  //创建可写流
  const createStrin = fs.createWriteStream("./foo.png", {
    flags: "a+"
  })

  request.on("data", (data) => {
    console.log(data)
    // 写入文件
    createStrin.write(data )
  })
  request.on("end", () => {
    console.log("数据传输完成")
	createStrin.close()//关闭文件
    response.end("OK")
  })
});

server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});

```

---

```bash
nodemon 上面的文件
```

---

在 PostMan 中发送 POST 请求，控制台得到的数据如下

 - 会发现存在多段数据，这就是如果文件过大，一个 on 不足于获取到所有文件。
 - 也可以更好的理解为什么多媒体也叫做流媒体，媒体就是一个非常大的文件，一次很难获取到所有的数据，所以就会是一个流，边观看边传递数据，这是在一个流中进行的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766144758000dlbfjn.png)

## 8.2 获取进度

```js
import http from "http";
import fs from 'fs'

const server = http.createServer((request, response) => {
  //创建可写流
  const createStrin = fs.createWriteStream("./foo.png", {
    flags: "a+"
  })
  //建立管道（request本质是一个可读流）
  request.pipe(createStrin)

  // 记录进度
  let curSize = 0
  const fileSize = request.headers["content-length"]

  request.on("data", (data) => {
    curSize += data.length
    // 写入文件
    createStrin.write(`文件上传的进度：${curSize/fileSize * 100}%\n`)
  })
  request.on("end", () => {
    response.end("文件上传成功")
    createStrin.close()//关闭文件
  })
});

server.listen(8000, () => {
  console.log("8000 端口服务器启动成功");
});

```

> [!warning] 上面上传都是错误的根本原因：
> - 没有确定上传的编码方式，以及写入的方式，导致文件乱码
> - 没有对 form-data 里面的数据进行分类整理，就全部放入到一个文件中
> 	- 里面有普通数据和图片，两种文件
> 	- 里面还包含了一些其他的数据，比如 boundary

## 8.3 正确做法片段

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176614776500050p0wg.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766147769000vr7ral.png)

## 8.4 html代码进行上传

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766149218000a7gm3j.png)



