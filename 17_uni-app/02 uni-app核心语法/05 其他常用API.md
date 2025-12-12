# 一、网络请求

https://uniapp.dcloud.net.cn/api/request/request.html#configmtls

uni.request(OBJECT) 发起网络请求。

 - 登录各个小程序管理后台，给网络相关的 API **配置合法域名**（域名白名单）
 - 微信小程序开发工具，在**开发阶段可以配置**：不校验合法域名
 - 运行到手机时，资源没有出来时可以打开手机的调试模式
 - 请求的 header 中 content-type 默认为 **application/json**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765437124000yr7i47.png)

# 二、数据缓存

https://uniapp.dcloud.net.cn/api/storage/storage.html

uni.setStorage(OBJECT)：将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，**这是一个异步接口**。

uni.setStorageSync(KEY, DATA)：将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，**这是一个同步接口**。

uni.getStorage(OBJECT)：从本地缓存中异步获取指定 key 对应的内容。

uni.getStorageSync(KEY)：从本地缓存中同步获取指定 key 对应的内容。

uni.removeStorage(OBJECT)：从本地缓存中异步移除指定 key。

uni.removeStorageSync(KEY)：从本地缓存中同步移除指定 key。


