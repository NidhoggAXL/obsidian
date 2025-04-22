# 一、jQuery的AJAX
在前端页面开发中，如果页面中的数据是需要动态获取或者更新的，这时我们需要向服务器发送异步的请求来获取数据，然后在无需刷新页面的情况来更新页面。那么**这个发起异步请求获取数据来更新页面的技术叫做AJAX。**

AJAX全称(AsynchronousJavaScriptAndXML)，是异步的JavaScript和 XML，它描述了一组用于构建网站和Web应用程序的开发技术

* 简单点说，就是使用 XMLHttpRequest对象与服务器通信。它可以使用 JON，XML，HTML 和 text 文本等格式发送和接收数据
* AJAX 最吸引人的就是它的“异步”特性。也就是说它可以在**不重新刷新页面的情况下与服务器通信，交换数据，或更新页面。**

AJAX请求方法(Method)

* GET、POST、PUT、PACTH、DELETE等


jQuery中也有AJAX模块，该模块是在XMLHttpRequest的基础上进行了封装，语法(Syntax)如下:

* `$`.ajax(`[settings]`)-默认用 GET 请求从服务器加载数据，会返回jQXHR对象，可以利用该对象的abort方法来取消请求。
* `$`.get( url `[,data][,success],dataType]`)-发起GET请求，底层调用的还是`$`ajax()
* `$`.post( url `[,data][,success][,dataType]`)-发起POST请求，底层调用的还是`$`ajax()

初体验jQuery中的AJAX: https://httpbin.org
(是一个专门提供:免费测试http服务的网站)


# 二、JAAX请求参数（parameters）
请求参数(Parameters)

* **url**-指定发送请求的 URL。
* **method/type**-用于指定请求的类型(e.g."POST","GET","PUT")，默认为GET
* **data**-指定要发送到服务器的数据(**PlainObject** or **String** or Array)
	* 什么是PlainObject？![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738566304000cy0jae.png)
* **processData**:当data是一个对象时,jQuery从对象的键/值对生成数据字符串，除非该procesData选项设置为false.例如，{a: "bc",d:"e,f“")被转换为字符串"a=bc&d=e%2Cf"，默认为true。
* **header**-请求头的内容(PlainObject)
* **contentType**-默认值:application/x-www-form-urlencoded; charset=UTF-8，向服务器发送数据时指定内容类型。
	* application/x-www-form-urlencoded; charset=UTF-8:请求体的数据以査询字符串形式提交，如:a=bc&d=e%2Cf
	* application/json; charset=UTF-8 指定为json字符串类型
	* 为时 false，代表是 multipart/form-data 。表单类型，一般用于上传文件
* **dataType** -期望服务器端发回的数据类型(json、xml、text.)，**默认会根据响应的类型来自动推断类型。**
* **timeout**-请求超时时间。它以毫秒为单位。
* **beforeSend**-这是一个在发送请求之前运行的函数，返回false会取消网路请求。
* **success**-请求成功回调的函数
* **error**-请求失败回调的函数

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738566239000go2u37.png)

# 三、AJAX基本请求
## 3.1 正确请求
```js
// 1.get请求
$.ajax({
 url: 'https://httpbin.org/get',
 type: 'get',//GET请求可以省略
 success: function(res) {
  console.log(res)
 }
})
  
//2.post请求
$.ajax({
 url: 'https://httpbin.org/post',
 type: 'post',
 success: function(res) {
  console.log(res)
 }
})
```

## 3.2 错误请求

500（后台代码异常）

503（服务器维护）

403（没有权限获取该资源）

404（路径错误）


```js
//500错误
$.ajax({
 url: 'https://httpbin.org/status/500',
 type: 'GET',
 error: function(error) {
  console.log(error)
 }
})
```

## 3.3 中途中断请求

服务器的7秒后返回数据，而我们发送的请求超时时间是5秒，我们在5秒前手动结束请求。

abort-中止、取消、流畅、夭折

```js
var jqXHR = $.ajax({
//服务器返回数据时间7秒
 url: 'https://httpbin.org/delay/7',
 method: 'POST',
 timeout: 5000,//超时时间是5秒
 error: function(error) {
  console.log(error)
 }
})


$('.btn').click(function() {
 jqXHR.abort()//手动取消请求
})
```

# 四、GET请求带参数
1. 直接在URL中添加

```js
$.ajax({
 url: 'https://httpbin.org/get?name=axl&age=18',
 method: 'GET',
 timeout: 5000,
 success: function(res) {
  console.log(res)
 }
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738572189000m2mba7.png)

2. 在data中提交参数

```js
$.ajax({
 url: 'https://httpbin.org/get',
 data: {
  name: 'axl',
  age: 18
 },
 method: 'GET',
 timeout: 5000,
 success: function(res) {
  console.log(res)
 }
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17385721290009qh171.png)


3. 给get提交请求头（获取权限）类似有VIP权限

```js
$.ajax({
 url: 'https://httpbin.org/get?name=axl&age=18',
 method: 'GET',
 headers: {
  token: 'axlVIP'
 },
 success: function(res) {
  console.log(res)
 }
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17385725420009m5x6e.png)


# 五、GET请求简写
jQuery 1.8 后的发行的编写方式

```js
$.get("https://httpbin.org/get")
 .then(function(){})//正确时的回调函数
 .catch(function(){})//错误时的回调函数
 .always(function(){})//最终都会执行的回调函数
```


# 六、POST请求带参数
1. 在url中提交查询字符串（很少）

```js
$.ajax({
 url: "https://httpbin.org/post?name=axl&age=19",
 method: "POST",
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738590125000rdhp8a.png)


2. 在data中提交查询字符串

```js
$.ajax({
 url: "https://httpbin.org/post",
 method: "POST",
 data: {
  name: 'axl',
  age: 18
 } 
})
```

请求的内容不会显式的表示在URL中

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738590162000mfx8n7.png)

想要查询的内容会放到**载荷**中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738590212000ne33t7.png)

3. 在data中JSON 字符串

```js
$.ajax({
 url: "https://httpbin.org/post",
 method: "POST",
 data: JSON.stringify ({
  name: 'axl',
  age: 18
 }),
 //告诉服务器发送的data是一个json类型数据
 contentType: "application/json; charset=UTF-8 "
})
```

查询的内容也不会显式的放到URL上面

同时查询内容会放到载荷，在响应（respose）中也可以看到：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738591512000m55hrp.png)

4. 在data中.FormData

```js
var forData = new FormData()
forData.append('name', 'axl')
forData.append('age', 18)
$.ajax({
 url: "https://httpbin.org/post",
 method: "POST",
 data: forData,
 processData: false,//processData:true,会将data为对象的转成查询宇符串
 contentType: false,//false的时候使用表单类型
})
```

查询的内容也不会显式的放到URL上面

同时查询内容会放到载荷，在响应（respose）中也可以看到：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738593430000a2gw0l.png)

5. 在添加请求头

```js
$.ajax({
 url: "https://httpbin.org/post",
 method: "POST",
 data: {
  name: 'axl',
  age: 18
 },
 headers: {
  user: 'aoao'
 }
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738593649000y9qwmg.png)


# 六、POST简写

```js
$.post('https://httpbin.org/post', {
 name: 'axl',
 age: 18
})
.then(function(){})
.catch(function(){})//错误时的回调函数
.always(function(){})//最终都会执行的回调函数
```
