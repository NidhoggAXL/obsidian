# 一、认识Storage

 WebStorage主要提供了**一种机制**，可以让浏览器提供一种**比cookie更直观的key、value存储方式**

  * **localStorage**：本地存储，提供的是一种**永久性的存储方法**，在关闭掉网页重新打开时，存储的内容依然保留； 
  * **sessionStorage**：会话存储，提供的是**本次会话的存储**，在关闭掉会话时，存储的内容会被清除；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732973354000m2noo8.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17329733750008o6ewi.png)

# 二、localStorage和sessionStorage的区别

我们会发现localStorage和sessionStorage看起来非常的相似。 

那么它们有什么区别呢？ 

* 验证一：**关闭网页后重新打开**，localStorage会保留，而sessionStorage会被删除； 
* 验证二：在**页面内实现跳转**，localStorage会保留，sessionStorage也会保留； 
* 验证三：在**页面外实现跳转**（打开新的网页），localStorage会保留，sessionStorage不会被保留；

一般在编写的时候代码：

```js
<script>
  let token = localStorage.getItem("token")
  if (!token) {
    token = "coderAxl is token"
    localStorage.setItem("token", token)
  }
  
  let username = localStorage.getItem("username")
  let password = localStorage.getItem("password")
  if (!username || !password) {
    username = "axl"
    password = 123456
    localStorage.setItem("username", username)
    localStorage.setItem("password", password)
  }
  console.log(token)
  console.log(username)
  console.log(password)
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17329741590009stq69.png)

# 三、Storage常见的方法和属性
Storage有如下的属性和方法： 

属性： 

* Storage.length：只读属性 
	* 返回一个整数，表示存储在Storage对象中的数据项数量；


方法： 

* Storage.key(index)：该方法接受一个数值n作为参数，返回存储中的第n个key名称； 
* Storage.getItem()：该方法接受一个key作为参数，并且返回key对应的value； 
* Storage.setItem()：该方法接受一个key和value，并且将会把key和value添加到存储中。 
	* 如果key存储，则更新其对应的值； 
* Storage.removeItem()：该方法接受一个key作为参数，并把该key从存储中删除； 
* Storage.clear()：该方法的作用是清空存储中的所有key；

# 四、localStorage工具封装

```js
<script>
  class Cache {
    constructor(isLocal = true) {
      this.storage = isLocal? localStorage: sessionStorage
    }
  
    setCache(key, value) {
      if (value) {
        //将对象转为字符串
        this.storage.setItem(key, JSON.stringify(value ))
      }
    }
  
    getCache(key) {
      const result = this.storage.getItem(key)
      if (result) {
        //将字符串转为对象
        return JSON.parse(result)
      }
    }
  
    removeCache(key) {
      localStthis.storageorage.removeItem(key)
    }
  
    clearCache() {
      this.storage.clear()
    }
  }
  
  const localCache = new Cache()
</script>

<script>
  let userInfo = {
    username: "axl",
    password: 123456
  }
  
  localCache.setCache("user", userInfo)
  console.log(localCache.getCache("user"))
  //{username: 'axl', password: 123456}
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1733040280000yt1krq.png)


