# 一 、网络请求

**Taro.request(OBJECT)** 发起网络请求。

 - 在各个小程序平台运行时，网络相关的 API 在使用前需要配置合法域名（域名白名单）。
 - 微信小程序开发工具在**开发阶段**可以配置：**不校验合法域名**。
 - header中的 content-type属性的默认值为：application/json

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765887614000hi59tu.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765887621000ca0eus.png)

# 二、数据缓存

**Taro.setStorage(OBJECT)**：将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个异步接口。

**Taro.setStorageSync(KEY, DATA)**：将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个同步接口。

**Taro.getStorage(OBJECT)**：从本地缓存中异步获取指定 key 对应的内容。

**Taro.getStorageSync(KEY)**：从本地缓存中同步获取指定 key 对应的内容。

**Taro.removeStorage(OBJECT)**：从本地缓存中异步移除指定 key。

**Taro.removeStorageSync(KEY)**：从本地缓存中同步移除指定 key。



