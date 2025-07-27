# 一、页面page配置文件
每一个小程序页面也可以使用 .json 文件来对本页面的窗口表现进行配置。 

* 页面中配置项在当前页面会覆盖 app.json 的 window 中相同的配置项。 
* https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/page.html

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753533632000j8rcrx.png)

# 二、配置案例实现

案例要求：

1. 在 page 的 favor 进行编写后，进行编译显示的时候先显示 favor 页面的内容
2. favor 页面默认显示 40 条列表，当页面滚动到离底部 50 的时候，会自动的添加 40 条列表
3. favor 页面下拉刷新的时候，一秒钟后，修改列表为 40 条

## 2.1 编译后默认显示某个页面

第一种方式：修改[[03 全局配置文件app.json|全局配置文件app.json]]的 pages （默认先加载和显示第一个页面）

```json
{
  "pages": [
    "pages/favor/favor",
    "pages/index/index"
  ]
}
```

第二种方式：在微信开发者工具中添加**编译模式**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753534478000md8vny.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753534628000fir76e.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753534654000h7ixri.png)

## 2.2 滚动到底部自动添加

favor 页面配置文件中（favor.json）添加：`"onReachBottomDistance": 50`

```json
{
  "usingComponents": {},
  "onReachBottomDistance": 50
}
```

favor 页面的逻辑文件中（favor.js）中编写逻辑：

```js
// pages/favor/favor.js
Page({
    data: {
        listCount: 40
    },

    //监听页面滚动到底部(是有自动排除tabBar高度的影响)
    onReachBottom() {
        console.log("滚动到了底部");
        this.setData({ listCount: this.data.listCount + 40})
    }
})
```

favor 页面的结构文件中（favor.wxml）中编写结构：

```html
<!--pages/favor/favor.wxml-->
<text>pages/favor/favor.wxml</text>
<block wx:for="{{listCount}}" wx:key="*this">
    <view>列表数据: {{item}} </view>
</block>
```

## 2.3 下拉修改data数据

favor 页面配置文件中（favor.json）添加：`"enablePullDownRefresh": true`

favor 页面的逻辑文件中（favor.js）中编写逻辑：

```js
// pages/favor/favor.js
Page({
    data: {
        listCount: 40
    },

    //监听页面滚动到底部(是有自动排除tabBar高度的影响)
    onReachBottom() {
        console.log("滚动到了底部");
        this.setData({ listCount: this.data.listCount + 40})
    },

    //监听页面下拉
    onPullDownRefresh() {
        //默认下拉是显示
        setTimeout(() => {
            //修改data的列表数据
            this.setData({ listCount: this.data.listCount = 40})
            //停止下拉显示
            wx.stopPullDownRefresh({
                success: (res) => {
                    console.log("停止成功", res);
                },
                fail:(err) => {
                    console.log("停止失败", err);
                }
            })
        }, 1000);
    }
    
})
```


