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


## 3.1 双线程时间轴对照-核心机制

图中左右两侧的纵向箭头代表时间流逝，横向箭头代表线程间通信（IPC）。必须对照着看，才能真正理解“什么时候渲染、什么时候能操作DOM”：

|时间节点|逻辑层（AppService）|渲染层（View）|关键动作与意义|
|---|---|---|---|
|**第1步**|`Start` -> `Create...`|`Start` -> `Init...`|页面开始创建，两线程初始化环境。|
|**第2步**|**`waiting notify...`**（阻塞等待）|`Init` -> **`waiting data...`**（阻塞等待）|**僵持状态**：逻辑层等视图层通知准备就绪，视图层等逻辑层下发数据。这是典型的**双向握手**。|
|**第3步**|收到通知，执行 **`onLoad`**|收到初始数据，执行 **`Send Initial Data`**|页面第一次接收到逻辑层传递的 `data`。此时视图层开始构建虚拟DOM。|
|**第4步**|执行 **`onShow`**|执行 `Notify...`（通知渲染完成）|页面显示，但**此时还未完成布局**。|
|**第5步（黄金节点）**|执行 **`onReady`**|执行 **`First Render`** 完成，**`Send Data`**（二次数据更新）|**这是最关键的一步**：`onReady` 触发代表**首屏渲染完毕**。此时你才可以通过 `wx.createSelectorQuery()` 获取节点宽高。|
|**第6步（后台）**|执行 **`onHide`**，随后 `set to background`|进入 `Rerender` 循环（可能因 `setData` 触发）|用户切到后台，页面不可见。注意：视图层仍在内存中，但渲染挂起。|
|**第7步（返回前台）**|执行 **`onShow`**|重新触发 `Rerender`|页面重新可见，逻辑层可能重新拉取数据。|
|**第8步（销毁）**|执行 **`destroy`** -> `onUnload`|执行 `End`|页面被回收，清除定时器和监听，释放内存。|

## 3.2 生命周期函数的底层原理与避坑指南

#### `onLoad` (只执行一次)

- **本质**：页面实例的“构造函数”。此时视图层尚未渲染。
    
- **用途**：接收上个页面传来的 `options` 参数，进行**初始数据赋值**。
    
- **注意**：**不要**在这里做 `wx.createSelectorQuery`，获取到的永远是 `null`。
    

#### `onShow` (多次执行)

- **触发**：页面显示时（首次进入、从后台切回、从其他页面 `navigateBack` 返回）。
    
- **你的误区**：很多人把数据请求全放在 `onLoad` 里，导致返回上一页再进来时数据没刷新。**正确做法**：如果页面数据依赖实时状态（如订单列表），**刷新请求应放在 `onShow` 中**。
    

####  `onReady` (只执行一次，且晚于 `onShow`)

- **本质**：图中 `First Render` 完成的信号。
    
- **意义**：这是**页面与视图层建立通信完成**的标志。
    
- **最佳实践**：所有涉及界面布局、节点操作（如 `createCanvasContext`、`createSelectorQuery().exec`）的代码，**必须**放在 `onReady` 或其之后触发的函数里。
    

#### `onHide` vs `onUnload`

- **`onHide`**：页面被遮挡（如切后台、打开新页面），**实例并未销毁**。视图层保持当前状态。
    
- **`onUnload`**：页面被销毁（如 `navigateBack` 或 `redirectTo`）。**必须**在此函数中清理全局监听（如 `EventBus.off`）、清除 `setInterval`，否则会造成内存泄漏。

## 3.3 图中“Rerender”与 `setData` 的深层关系

图中视图层出现了多次 `Rerender` 和 `Send Data`，这对应着 `this.setData()` 的调用：

1. **初始数据（Init Data）**：逻辑层将第一次 `data` 传给视图层，视图层构建影子树（Shadow Tree）。
    
2. **增量更新**：当你调用 `this.setData()` 时，逻辑层只会把**变化的那部分数据**（Diff 数据）发送给视图层，视图层进行局部 `Rerender`。
    
3. **性能陷阱**：图中多次 `Rerender` 暗示了高频 `setData` 的风险。如果频繁调用，视图层会不断重新计算布局。**建议**：合并多次 `setData` 为一次对象更新，避免传递过大的数据（建议单次 < 256KB）。

## 34 总结：开发时的“黄金执行顺序”

如果你在开发中搞不清顺序，请记住这个硬核结论：

> **`onLoad` -> `onShow` -> (等待视图初始化) -> `onReady` -> (视图渲染完成，可以操作UI)**

**最后的忠告**：图中 `AppService` 有 `waiting notify` 而 `View` 有 `waiting data`，这说明**逻辑层执行会阻塞视图层首次渲染**。因此，**永远不要在 `onLoad` 或 `onShow` 中执行同步的、耗时的 CPU 密集计算**（如大量循环解密数据），否则会导致首屏白屏时间延长。应将这些计算拆解到异步任务中，或放在 `onReady` 之后执行。

