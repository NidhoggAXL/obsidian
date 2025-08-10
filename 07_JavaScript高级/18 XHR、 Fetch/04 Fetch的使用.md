# 一、认识Fetch和Fetch API
Fetch可以看做是早期的XMLHttpRequest的替代方案，它提供了一种更加现代的处理方案： 

* 比如**返回值是一个Promise**，提供了一种更加优雅的处理结果方式 
	* 在请求发送成功时，调用resolve回调then； 
	* 在请求发送失败时，调用reject回调catch； 
* 比如**不像XMLHttpRequest一样**，所有的操作都在一个对象上；

fetch函数的使用：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17339088950001tzx4s.png)

* **input**：定义要获取的资源地址，可以是一个URL字符串，也可以使用一个Request对象（实验性特性）类型； 
* **init**：其他初始化参数 
	* **method**: 请求使用的方法，如 GET、POST； 
	* **headers**: 请求的头信息； 
	* **body**: 请求的 body 信息；

```js
fetch(url, {
	methiod: "post",
	heders: {},
	body: 
})
```

# 二、Fetch数据的响应（Response）
**Fetch的数据响应主要分为两个阶段：** 

阶段一：当服务器返回了响应（response） 

* fetch 返回的 promise 就使用内建的 Response class 对象来对响应头进行解析； 
* 在这个阶段，我们可以通过检查响应头，来检查 HTTP 状态以确定请求是否成功； 
* 如果 fetch 无法建立一个 HTTP 请求，例如网络问题，亦或是请求的网址不存在，那么 promise 就会 reject； 
* 异常的 HTTP 状态，例如 404 或 500，不会导致出现 error；

我们可以在 response 的属性中看到 HTTP 状态： 

* status：HTTP 状态码，例如 200； 
* ok：布尔值，如果 HTTP 状态码为 200-299，则为 true； 

第二阶段，为了获取 response body，我们需要使用一个其他的方法调用。

* response.text() —— 读取 response，并以文本形式返回 response；
* response.json() —— 将 response 解析为 JSON；

# 三、Fetch网络请求的演练
基于Promise的使用方案：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733909473000nhnr8s.png)

基于async、await的使用方案：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733909482000r5eu57.png)

# 四、Fetch POST请求
创建一个 POST 请求，或者其他方法的请求，我们需要使用 fetch 选项： 

* method：HTTP 方法，例如 POST， 
* body：request body，其中之一： 
	* 字符串（例如 JSON 编码的）， 
	* FormData 对象，以 multipart/form-data 形式发送数据，

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733909568000d646sj.png)


# 五、Fetch 优化过程(了解)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733909755000ptbqqk.png)






