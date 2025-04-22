# 一、jQuery对文本的操作
**.text()、.text(text)**

* 获取**匹配到元素集合中每个元素**组合的文本内容，包括它们的后代，或设置匹配到元素的文本内容。
* 相当与原生元素的textContent属性。

```js
  <script>
  //1.监听文档解析完成
  $(function() {
   console.log($('ul li').text())
   //li-1li-2li-3li-4li-5
  
   $('ul li').text('aoao')
  })
 </script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737802406000urlaef.png)


**.html()、html(htmlString)**

* 获取**匹配到元素集合中第一个元素**的**HTML内容**，包括它们的后代，或设置每个匹配元素的 HTML 内容:
* 相当与原生元素的innerHTML属性。

```js
 <script>
  //1.监听文档解析完成
  $(function() {
   console.log($('ul li').html())//li-1
  
   $('ul li').html('lalal')
  })
 </script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737802545000v7i3pl.png)


```js
 <script>
  //1.监听文档解析完成
  $(function() {
   $('ul li').html(
    `
     <span>我是span</span>
     <div>我是div</div>
    `
   )
  })
 </script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737802671000c3jzsj.png)


**.val()、.val(value)**

* 获取匹配到元素集合中第一个元素的当前值 或 设置每个匹配到元素的值。
* 该.val()方法主要**用于获取input,select和等表单元素的值。**
* 相当与获取原生元素的value属性。

```js
 <input type="text" class="user">
 <input type="text" class="password">
 <button class="btn">登陆</button>
  
 <script src="../libs/jquery-3.6.0.js"></script>
 <script>
  $('.btn').click(function() {
   console.log($('.user').val())//aoao
   console.log($('.password').val())//123456
  })
 </script>
```


# 二、jQuery对CSS的操作
**.width()、.width(value)**

* 获取匹配到元素集合中**第一个元素的宽度**或设置每个匹配到元素的宽度。

**.height()、height(value)**

* 获取匹配到元素集合中**第一个元素的高度**或设置每个匹配到元素的高度。

**css(propertyName)、.css(propertyNames)**

* 获取匹配到元素集中**第一个元素样式属性的值**，底层是调用getComputedStyle函数获取。**compute-计算**
* .css("width")和.width()之间的区别
	* width()返回一个无单位的像素值(例如，400)，而css()返回一个具有完整单位的值(例如，400px)

```js
 <script>
  //1.监听文档解析完成
  $(function() {
   console.log($('ul').width())//100
   console.log($('ul').css("width"))//100px
  })
 </script>
```

# 三、jQuery对Class属性的操作
**.addClass(className)、.addClass(classNames)、.addClass(funcntion)**

* 将指定的类添加到匹配元素集合中的每个元素，每次都是追加class。
* 底层调用的是[[07 元素的属性(property)|setAttribute]]("class",finalValue )方法添加class.


**.hasClass(className)**

* 是否给任意匹配到的元素分配了该类。
* 底层是通过getAttribute("class").indexOf()来判断是否存在

**removeClass()、.removeClass(className)、.removeClass(classNames)、.removeClass(function)**

* 给匹配元素集中的**每个元素删除单个类、多个类或所有类。**
* 底层调用的是setAttribute("class",finalValue )方法。

**`toggleClass()、.toggleClass(className[,state])、.toggleClass(classNames[,state])`**

* 根据类的存在或状态参数的值，在匹配到元素的集合中，给**每个元素添加或删除一个或多个类**

# 四、attributes和property属性的操作

attributes: 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737866868000u3hsap.png)

property:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737866878000il2xp6.png)


**.attr(attributeName)**

* 获取匹配元素集和中**第一个元素**的属性值，底层调用了原生的 getAttribute()API


**.attr(attributeName, value)、.attr(attributes)**

* 为每个匹配元素**设置一个或多个属性**，底层调用了原生的 setAttribute() API


**.removeAttr(attributeName)**

* 在匹配到元素的集中，给每个元素删除一个属性,底层调用了原生的 removeAttribute()API

**.prop(propertyName)**

* 获取匹配到元素集合中**第一个元素**的属性值

**.prop(propertyName,value)、.prop(propertys)**

* 为每个匹配元素设置一个或多个属性。

**removeProp(propertyName)**

* 删除匹配元素集的属性，只能删除用户自定义添加的prop，**不能删除元素本身的属性 )。**


# 五、自定义data-xx属性的操作

> [!tip] data-xx的缓存
> 当我们使用jQuery的操作获取data-xxx的时候，会吧data-xxx的数据进行一个缓存，是缓存到获取元素的对象上面。
> 进行获取操作了才会缓存，没有进行data操作不会缓存

**.data()、.data(key)**

* 获取匹配元素集中**第一个元素**的自定义属性的值
* 并把data-xxx进行缓存

不进行缓存：

```js
console.log("%O",$('ul').get(0))
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/173789488500072945k.png)


进行缓存：

```js
console.log("%O",$('ul').get(0))
console.log($('ul').data('age'))//18
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17378948500008bjhdx.png)


**.data(key, value)、.data(obj)**

* 为每个匹配元素设置**一个或多个**自定义属性
* 设置缓存上面的值，并不能改变属性上面的值

**.removeData([namel])**

* 会删除data()函数给匹配元素属性添加的数据 和 data()函数绑定的自定义属性。
* data函数添加的属性会被移除，**但是如果属性同时在签上定义了就不会被移除。**

 
