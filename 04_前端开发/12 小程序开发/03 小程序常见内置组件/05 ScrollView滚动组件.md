# 一、scroll-view组件解析
scroll-view可以实现局部滚动，常见属性如下：

* https://developers.weixin.qq.com/miniprogram/dev/component/scroll-view.html

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17536065700002tcd4g.png)

> [!important] 注意事项： 
> * 实现滚动效果必须添加scroll-x或者scroll-y属性（只需要添加即可，属性值相当于为true了） 
> * 垂直方向滚动**必须设置**scroll-view一个高度

# 二、案例

页面横向滚动（x 轴滚动），检测滚动到最右边和最左边

> [!note] 想要在 scroll-view 上面进行 flex 布局的时候，要使用 enable-flex 属性

```html
<!--pages/scroll/scroll.wxml-->
<scroll-view 
  class="container" 
  scroll-x 
  enable-flex
  bindscrolltoupper="onScrollUpper"
  bindscrolltolower="onScrollLower"
  bindscroll="onScroll"
>
  <block wx:for="{{itemColor}}" wx:key="*this">
    <view class="item" style="background-color: {{item}};">{{item}}</view>
  </block>
</scroll-view>
```

```js
// pages/scroll/scroll.js
Page({
  data: {
    itemColor: ["blue", "red", "gold", "navy", "purple"]
  },
  
  // 监听scroll-view滚动
  onScrollUpper() {
    console.log("滚动到顶部或者左边");
  },
  onScrollLower() {
    console.log("滚动到底部或者右边");
  },
  onScroll(event) {
    console.log("scroll-view：滚动", event);
  }
})
```

```css
/* pages/scroll/scroll.wxss */
.container {
  display: flex;
  background-color: yellow;
}

.item {
  width: 100px;
  height: 100px;
  /* 防止被压缩 */
  flex-shrink: 0;
}
```

> [!tldr] 内容补充：
> - scroll-view 有默认高度 120px
> - scroll-view 要使用 flex 布局，要添加 enable-flex 属性
> - container 的 class 在 app.wxss 中有默认添加这个 class




