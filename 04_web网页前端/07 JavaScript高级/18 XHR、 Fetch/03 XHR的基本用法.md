# 一、AJAX发送请求
 **AJAX 是异步的 JavaScript 和 XML（Asynchronous JavaScript And XML）** 
 
 * 它可以使用 JSON，XML，HTML 和 text 文本等格式发送和接收数据；
 
 如何来完成AJAX请求呢？ 
 
 * 第一步：创建网络请求的AJAX对象（使用**XMLHttpRequest**） 
 * 第二步：监听XMLHttpRequest对象状态的变化，或者监听onload事件（请求完成时触发）； 
 * 第三步：配置网络请求（通过**open**方法）； 
 * 第四步：发送**send**网络请求；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733750106000r5imhb.png)

 
# 二、XMLHttpRequest的state（状态）
事实上，我们在一次网络请求中看到状态发生了很多次变化

```js
<script>
  // 创建XMLHttpRequest对象
  const xhr = new XMLHttpRequest()
  
  xhr.onreadystatechange = function() {
    console.log(xhr.readyState)
  }
  
  //配置请求open
  xhr.open("get", "http://123.207.32.32:8000/home/multidata")

  xhr.send()
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17337521950005ho9ac.png)


这是因为对于一次请求来说包括如下的状态：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733752245000x585de.png)

> [!tip] 注意：
> 这个状态并非是HTTP的相应状态，而是记录的XMLHttpRequest对象的状态变化。 
> * http响应状态通过status获取；

**AJAX 发送请求默认是一个异步请求**

同步请求和异步请求的区别：

```js
xhr.end("get","url")
console.log("++++")
console.log("----")
```

>**同步请求**：只有等 xhr.end 发送请求得到全部数据后**才会**执行后面的打印代码
>**异步请求**：**不需要**等到得到全部数据，会先指向后面的打印代码

# 三、XMLHttpRequest其他事件监听
除了onreadystatechange还有其他的事件可以监听 

* **loadstart**：请求开始。 
* **progress**： 一个响应数据包到达，此时整个 response body 都在 response 中。 
* **abort**：调用 xhr.abort() 取消了请求。 
* **error**：发生**连接错误**，例如，域错误。不会发生诸如 404 这类的 HTTP 错误。 
* **load**：请求成功完成。 
* **timeout**：由于请求超时而取消了该请求（仅发生在设置了 timeout 的情况下）。 
* **loadend**：在 load，error，timeout 或 abort 之后触发。

我们也可以使用load来获取数据：

```js
xhr.onload = function() {
	console.log(xhr.response)
}
```

# 四、响应数据和响应类型
发送了请求后，我们需要获取对应的结果：response属性 

* XMLHttpRequest **response属性** 返回响应的正文内容； 
* 返回的类型取决于r**esponseType**的属性设置；

通过responseType可以设置获取数据的类型 

* 如果将 responseType 的值设置为空字符串，则会使用 **text作为默认值**

```js
xhr.responseType = "json"
```

和responseText、responseXML的区别： 

* **早期通常服务器**返回的数据是**普通的文本和XML**，所以我们通常会通过responseText、 responseXML来获取响应结果； 
* 之后将它们转化成JavaScript对象形式； 
* 目前服务器基本返回的都是**json数据**，直接设置为json即可；


# 五、HTTP响应的状态status
**XMLHttpRequest的state是用于记录xhr对象本身的状态变化，并非针对于HTTP的网络请求状态。** 

如果我们希望获取**HTTP响应的网络状态**，可以通过status和statusText来获取：

```js
console.log(xhr.status)
console.log(xhr.statusText)
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733820266000mqox8t.png)

# 六、GET/POST请求传递参数
在开发中，我们使用最多的是GET和POST请求，在发送请求的过程中，我们也可以传递给服务器数据。

常见的传递给服务器数据的方式有如下几种： 

* **方式一**：GET请求的query参数 
* **方式二**：POST请求 FormData 格式 
* **方式三**：POST请求 JSON 格式
* **方式四**：POST请求 x-www-form-urlencoded 格式 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733830841000l3rord.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733830900000ia953b.png)


# 七、AJAX网络请求封装(了解)
**在开发中有非常好的工具库来使用，这里了解这个思路就好**

```js
<script>
  function xlajax({
    url,
    method = "get",
    data = {},
    sucess,
    failure
  } = {}) {
    //1.监听对象
    const xhr = new XMLHttpRequest()
  
    //2.监听数据
    xhr.onload = function() {
      //通过 HTTP 的状态来判断执行那个回调函数
      if (xhr.status >= 200 && xhr.status < 300) {
        //把成功的结果回调到 sucess 里面去
        //并且sucess要存在，才可以回调回去数据
        sucess && sucess(xhr.response)
      } else {
        //和成功一样要存在failure才可以回调
        failure && failure({ status: xhr.status, message: xhr.statusText})
      }
    }
  
    //3.设置数据类型
    xhr.responseType = "JSON"
  
    //4.配置open
    //4.1 GET 和 POST 方法的选择
    if (method.toUpperCase() === "GET") {
      //get 请求 不管get是大小写
      //toUpperCase转换为大写
      const queryStrings = []
      //获取 data 里面的数据
      for (const key in data) {
        queryStrings.push(`${key}=${data[key]}`)
      }
      url = url + "?" + queryStrings.join("&")
      xhr.open(method, url)
      xhr.send()
    } else {
      //POST 请求
      xhr.open(method, url)
      //配置 POST 请求头
      xhr.setRequestHeader("Content-Type", "application/json")
      //将data对象转换为 JSON 的字符数据
      xhr.send(JSON.stringify(data))
    }
  }
  

  xlajax({
    url : "http://123.207.32.32:1888/02_param/get",
    method : "get",
    data: {
      name: "axl",
      age: 18
    },
    sucess: function(res) {
      console.log("res:", res)
    },
    failure: function(err) {
      // console.log("err:", err)
    }
  })
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733906259000h7hgno.png)

这里如果请求成功还是发送网络请求，容易产生回调地狱，这里可以返回一个 Promise

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733907057000bsourc.png)

# 八、延迟时间timeout和取消请求
在网络请求的过程中，为了避免过长的时间服务器无法返回数据，通常我们会为请求设置一个超时时间：**timeout**。 

* 当达到超时时间后依然没有获取到数据，那么**这个请求会自动被取消掉**； 
* 默认值为0，表示没有设置超时时间； 

我们也可以通过**abort方法**强制取消请求；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733907983000vev8ur.png)

