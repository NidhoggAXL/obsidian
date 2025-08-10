在开发中，某些常见我们需要将一部分数据存储在本地：比如token、用户信息等。 

- 小程序提供了专门的Storage用于进行本地存储。

同步存取数据的方法：

- wx.setStorageSync(string key, any data) 
- any wx.getStorageSync(string key) 
- wx.removeStorageSync(string key) 
- wx.clearStorageSync()

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1753796003000ytdxuw.png)


异步存储数据的方法： 

- wx.setStorage(Object object) 
- wx.getStorage(Object object) 
- wx.removeStorage(Object object) 
- wx.clearStorage(Object object)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1753796007000vxg6es.png)


