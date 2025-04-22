# 一、认识jQuery函数
jQuery是一个**工厂函数**( 别名`$`)-类似与new操作的函数，调用该函数，会根据传入参数类型来返回**匹配到元素的集合**，一般把该集合称为**jQuery对象**。

* 如果传入假值:返回一个**空的集合。**
* 如果传入选择器:返回在**在documnet中所匹配到元素的集合。**
* 如果传入元素:返回包含**该元素的集合。**
* 如果传入HTML字符串，返回包含**新创建元素的集合**
* 如果传入回调函数:返回的是**包含document元素集合,并且当文档加载完成会回调该函数**
* 因为函数也是对象，所以该函数还包含了很多已封装好的类方法。如:`jQuery.noConflict`、`jQuery.ready`等

```js
<script src="../libs/jquery-3.6.0.js"></script>
<script>
 //1.假值：'' null undefined NAN false ……
 console.log(jQuery(''))
  
 //2.字符串（选择器）
 console.log(jQuery('body'))
  
 //3.字符串（html）
 console.log(jQuery('<div>'))
 var $els = jQuery( `
  <div>我是div元素</div>
 `)
 $els.appendTo('body')
 console.log($els)
  
 //4.元素类型
 var bodyEl = document.querySelector('body')
 console.log(jQuery(bodyEl))
  
 //5.监听文档解析完成
 var $doc =
 jQuery(function() {
  console.log("文档解析完成")
 })
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737624289000v614sc.png)

# 二、认识jQuery对象
jQuery对象是一个包含所**匹配到元素的集合**，该集合是**类数组(array-like)对象,**

* jQuery对象是通过**调用jQuery函数来创建的**
* jQuery对象中会**包含`N(>=0)`个匹配到的元素**
* jQuery 对象**原型中包含了很多已封装好的方法。**例如:DOM操作、事件处理、动画等方法。

下面我们通过调用jQuery函数来新建一个jQuery对象，例如:
* `$()` 新建一个空的jQuery对象
* `$(document)`新建一个包含document元素的jQuery对象
* `$('选择')`新建一个包含所选中DOM元素的jQuery对象

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737632450000lto3f7.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737632460000ep2w87.png)


# 三、jQuery对象与DOM Element的区别
jQuery对象与DOM Element的区别

* 获取的方式不同
	* DOM Element 是通过原生方式获取，例如:document.querySelector()
	* jQuery对象是通过调用jQuery函数获取，例如:jQuery(‘div')
* jQuery对象是一个**类数组对象**，该对象中**会包含所选中的DOM Element的集合,**
* jQuery对象的原型上扩展非常多实用的方法，DOM Element 则是W3C规范中定义的属性和方法。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737633178000un3m3s.png)

# 四、jQuery对象与DOM Element的相互装换
**jQuery对象转成DOM Element**

* `.get(index)`: 获取jQuery 对象中某个索引中的 DOM 元素。
	* index一个从零开始的整数，指示要检索的元素
	* 如果index超出范围(小于负数元素或等于或大于元素数)，则返回undefined。
* `.get()`:没有参数，将返回jQuery对象中所有DOM元素的**数组**

```html
<ul class="panel">
 <li class="item1"></li>
 <li class="item2"></li>
 <li class="item3"></li>
 <li class="item4"></li>
 <li class="item5"></li>
</ul>
<script src="../libs/jquery-3.6.0.js"></script>
<script>
 //1.监听文档解析完成
 $(function() {
  var $list = $('ul li')
  console.log($list.get())
  //[li.li-1, li.li-2, li.li-3, li.li-4, li.li-5]
   for (var item of $list.get()) {
    console.log(item)
   }
 })
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737814826000tgjpqn.png)

**DOM Element转成jQuery对象**

* 调用jQuery函数或者$函数
* 例如:$(元素)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737634253000xcrbgp.png)


