
# 一、注册页面-Page函数

小程序中的每个页面, 都有一个对应的js文件, 其中调用**Page函数**注册页面示例 

* 在注册时, 可以**绑定初始化数据、生命周期回调、事件处理函数**等。 
* https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html 

我们来思考：注册一个Page页面时，我们一般需要做什么呢？ 

1. 在**生命周期函数**中发送网络请求，从服务器获取数据； 
2. **初始化一些数据**，以方便被wxml引用展示； 
3. **监听wxml中的事件**，绑定对应的事件函数； 
4. 其他一些**监听**（比如页面滚动、上拉加载、下拉刷新更多等）；；

# 二、注册Page时做什么？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753579808000tla2nn.png)

# 三、Page页面的生命周期

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17535800140002xaxws.png)




