# 一、jQuery动画操作-animate
.animate(): 执行一组 CSS属性的自定义动画，允许支持**数字的CSS属性(底层是调用JS)**上创建动画

* `.animate( properties [, duration ][, easing ][, complete ])`
* .animate( properties, options) - options对象的意思
	* propertys参数的支持:
		* 数值:number、string
		* 关键字:'show(显式)'、'hide(隐藏)'和'toggle(切换)'
		* 相对值:+=、
		* 支持 em、%单位(可能会进行单位转换)- 如果是50%，那么就会**恢复到父元素的50%，而不是自己的50%**
	* duration参数支持：（可选）
		* 数值：number（单位是毫秒）
		* 关键字：slow(600毫秒)、fast(200毫秒)
	* easing参数支持：（可选）
		* 关键字：linear（默认）、swing
	* complete回调函数（可选）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738506180000cugkt3.png)

```js
//.animate( properties [, duration ][, easing ][, complete ])
$('div').animate({
 opacity: 0,
 height: 0,
 // height: 0% //相对父元素
 // height: 'hide' //隐藏
 // height: '+=40px' //在原来的基础上加上40p
}, 400, 'swing', function() {
 console.log("发生了动画的改变")
})
```

# 二、jQuery常见动画函数
**显示和隐藏匹配的元素**

* .hide()、.hide( `[duration][,complete]`)、.hide(options)- 隐藏元素
* .show()、.show( `[duration][,complete]`)、.show( options)-显示元素
* .toggle()、.toggle(`[duration][,complete]`)、.toggle(options)-切换显示或者隐藏元素

**淡入淡出**

* .fadeln()、.fadeln( `[duration][, complete]`)、 .fadeln( options)-淡入动画
* .fadeOut()、.fadeOut( `[duration][,complete]`)、.fadeOut( options )-淡出动画淡入淡出的切换
* .fadeToggle()、.fadeToggle( `[duration ][, complete ]`)、.fadeToggle( options )
* .fadeTo( duration,opacity`[,complete]`)-渐变到

# 三、jQuery元素中的动画队列
jQuerv匹配元素中的**animate**和**delay**动画是通过一个**动画队列(queue)** 来维护的。 例如执行下面的动画都会添加到动画队列中:

* .hide()、.show()
* .fadeln()、.fadeOut()
* .animate()、delay()
* ……

**.queue()**:查看当前选中元素中的动画队列。

**.stop(`[clearQueue][,jumpToEnd]`)**:停止匹配元素上当前正在运行的动画

* clearQueue :一个布尔值，指示是否也删除排队中的动画。默认为false
* jumpToEnd :一个布尔值，指示是否立即完成当前动画。默认为false

```js
$('.box').animate({
 top: 100
})

$('.box').animate({
 left: 100
})

$('.box').animate({
 top: 0
})

$('.box').animate({
 left: 0
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738558469000qkjswp.png)


# 四、侧边栏隐藏小案例
点击右上角的×，这个侧边栏会先向下移动完灰色消失，在向右移动完全部内容，并且把整个图标隐藏。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738562012000rbazuc.png)


```html
<style>
 .box {
  position: fixed;
  bottom: 0;
  right: 0;
 }
  
 img {
  vertical-align: bottom;
 }
  
 .btn {
  position: absolute;
  top: 5px;
  right: 0;
  width: 25px;
  height: 25px;
  /* border: 1px solid red; */
 }
</style>

<div class="box">
 <div class="top">
  <span class="btn"></span>
  <img src="./images/top.png" alt="">
 </div>
 <div class="bottom">
  <img src="./images/bottom.png" alt="">
 </div>
</div>

<script>
$('.btn').click(function() {
 $('.bottom').animate({height: 0}, 600, function() {
  $('.box').animate({width: 0}, 600, function() {
   //diaplay: none 不是数值类型所以不可以通过jQuery的动画进行设置
   //只可以通过css进行设置
   $('.box').css('display', 'none')
  })
 })
})
</script>
```

