# 一、注册小程序-App函数

每个小程序都需要在 app.js 中调用 App 函数 注册小程序实例 

* 在注册时, 可以绑定对应的生命周期函数； 
* 在生命周期函数中, 执行对应的代码； 
* https://developers.weixin.qq.com/miniprogram/dev/reference/api/App.html


我们来思考：注册App时，我们一般会做什么呢？ 

* **判断小程序的进入场景** 
* **监听生命周期函数**，在生命周期中执行对应的业务逻辑，比如在某个生命周期函数中进行登录操作或者请求网络数据； 
* **因为App()实例只有一个**，并且是全局共享的（单例对象），所以我们可以将一些共享数据放在这里；

# 二、作用一：判断打开场景

小程序的打开场景较多： 

* 常见的打开场景：群聊会话中打开、小程序列表中打开、微信扫一扫打开、另一个小程序打开 
* https://developers.weixin.qq.com/miniprogram/dev/reference/scene-list.html

如何确定场景? 

* 在onLaunch和onShow生命周期回调函数中，会有**options参数**，其中有**scene值**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753540252000sszlf9.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753539647000gt1v2e.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753539661000t06wug.png)

## 2.1 模拟进入场景(不是启动)

点击模拟器的关闭小程序，就会跳出要选择的进入的场景

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753540428000h5ve0u.png)


# 三、作用二：定义全局App的数据

可以在Object中定义全局App的数据：

```js
// app.js
App({
    globalData: {
        token: "axlToken",
        userInfo: {
	        nickname: 'axl',
	        leave: 99
        }
    }
})
```

定义的数据可以在其他任何页面中访问：

```js
Page({
    //获取app.js定义的全局数据
    onLoad() {
        const app = getApp()
        console.log(app.globalData.token);//alxToken
        console.log(app.globalData.userInfo);//{nickname: "axl", leavl: 99}
    }
})
```

# 四、作用三 – 生命周期函数

在生命周期函数中，完成应用程序启动后的初始化操作

* 比如[[06 小程序登录流程|登录操作]]； 
* 比如读取本地数据（类似于token，然后保存在全局方便使用） 
* 比如请求整个应用程序需要的数据；

```js
// app.js
App({
    //定义全局
    globalData: {
        token: "",
        userInfo: {}
    },
    onLaunch(options) {
        //0.获取本地保存的Storage
        const token = wx.getStorageSync('token')
        const userInfo = wx.getStorageSync('userInfo')
        console.log(token, userInfo);

        //1.进行登录
        if( !token || !usrInfo ) {
            wx.setStorageSync('token', "axlToken")
            wx.setStorageSync('usreInfo', { nickname: 'axl', leavl: 100 })
        }

        //2.保存登录数据
        this.globalData.token = token
        this.globalData.userInfo = userInfo

        //3.发送网络请求,获取数据
        wx.request({
          url: 'url',
        })
    },
})

```
