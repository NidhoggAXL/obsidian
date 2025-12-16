# 一、页面生命周期

Taro 页面组件除了支持 **React 组件生命周期** 方法外，还根据小程序的标准，额外支持以下**页面生命周期**：

 - onLoad (options) 在小程序环境中对应页面的 onLoad。
	 - 通过访问 options 参数或调用 getCurrentInstance().router，可以访问到页面路由参数
 - componentDidShow() 在小程序环境中对应页面的 onShow。
 - onReady () 在小程序环境中对应页面的 onReady。
	 - 可以使用 createCanvasContext 或 createSelectorQuery 等 API 访问小程序渲染层 DOM 节点
 - componentDidHide () 在小程序环境中对应页面的 onHide。
 - onUnload () 在小程序环境中对应页面的 onUnload
	 - 一般情况下建议使用 React 的 componentWillUnmount 生命周期处理页面卸载时的逻辑。
 - onPullDownRefresh() 监听用户下拉动作。
 - onReachBottom() 监听用户上拉触底事件。
 - 更多生命周期函数： https://docs.taro.zone/docs/react-page

# 二、Hooks生命周期

Taro使用Hooks很简单。Taro专有Hooks，例如 `usePageScroll`, `useReachBottom`，需从 @tarojs/taro 中引入

React框架自己的 Hooks ，例如 `useEffect`, `useState`，从对应的框架引入。

更多的Hooks可查看官网： https://docs.taro.zone/docs/hooks

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765887524000n331gf.png)




