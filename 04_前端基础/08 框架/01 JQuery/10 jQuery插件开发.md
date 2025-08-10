# 一、认识jQuery插件
在我们开发时，有时候jQuery提供的方法并不能满足我们的需求。如果我们想给jQuery扩展一些其它的方法，那这种情况下可能需要编写一个插件(**plugins**)。

* jQuery插件其实就是:编写一些新增的方法，并将这些方法添加到jQuery的原型对象上。

编写jQuery 插件的步骤:

* 新建一个插件对应的JS文件(命名规范:jquery.插件名.js)
* 在立即执行函数中编写插件，这样可以避免插件中的变量与全局变量冲突
* 在jQuery的原型对象上新增一些的方法
* 最后在html中导入就可以像使用其他jQuery对象方法一样使用了
* 到此就开发完一个iQuery的插件了，

# 二、小案例
对a元素添加a元素对应的URL到后面，并对URL天机括号

工具的封装：

```js
;(function(window, $) {

 $.fn.showlinklocation = function() {
  //防止不是a对象，进行过滤后在遍历
  this.filter("a").each(function() {
   // console.log(this)//DOM Element
   let axHref = $(this).attr('href')//获取attribute属性中的 href
   $(this).append(`(${axHref})`)
  })
 }
 return this //这里的this是jQuery对象
  
})(window, jQuery)
```


工具的使用：

```html
<a href="https:www.jd.com">京东商城</a>
<a href="https:www.taobao.com">淘宝商城</a>

<script src="../libs/jquery-3.6.0.js"></script>
<script src="./utils/01 网址查看.js"></script>

<script>
 //1.监听文档解析完成
 $(function() {
  $('a').showlinklocation()
 })
</script>
```

效果图：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738596458000wtpcrc.png)



