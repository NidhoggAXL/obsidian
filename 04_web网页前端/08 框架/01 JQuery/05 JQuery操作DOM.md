# 一、jQuery的DOM操作-插入内容
## 1.1 插入内容一

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737964675000tj3faw.png)

`.append(content[,content])、append( function )`

* 将**参数的内容**插入到匹配元素集中每个元素的**末尾**
* content 的类型: DOM element, text node, array of elements and text nodes, HTML string, or jQuery object

```js
//1.DOM Element
var liEl = document.createElement("li")
liEl.className = "li-6"
liEl.innerHTML = "li-6"
$('ul').append(liEl)
  
//2.text node
$('ul').append("li-6")
  
//3.array of elements and text nodes
$('ul').append(["li-6", "li-7"])
  
//4.HTML string
$('ul').append(`
 <li>li-6</li>
 <li>li-7</li>
`)
  
//5.jQuery object
var $el = $('<li>').addClass('li-6').text('li-6')
$('ul').append($el)

//6.选择页面上面的元素进行插入
$('ul').append($('.li-6'))
//移动.li-6，并不是移动
```

`.prepend(content[,content])、prepend( function )`

* 将参数的内容插入到匹配元素集中每个元素的**开头**。

`.after(content [,content])、after( function )`

* 在匹配元素集中的每个元素**之后**，插入由参数指定的内容，

`.before(content [, content])、before( function )`

* 在匹配元素集中的每个元素**之前**，插入由参数指定的内容。


## 1.2 插入内容二
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738477255000vcy69x.png)

**.appendTo(target)**

* 将匹配元素集中的**每个元素**插入到**目标元素的末尾**
	* target的类型:A selector, element, HTML string, array of elements, or jQuery object.

**.prependTo(target)**

* 将匹配元素集中的每个元素插入到**目标元素的开头**

**.insertAfter(target)**

* 在**目标元素之后**，插入匹配元素集中的每个元素。

**.insertBefore(target)**

* 在**目标元素之前**，插入匹配元素集中的每个元素。

```js
//1.jQuery参数
$('<li>').addClass('li-6').text('我是li-6').appendTo( $('ul') )
  
//2.字符串参数
$('<li>').addClass('li-6').text('我是li-6').appendTo('ul')
  
//3.DOM元素操作
const ulEl = document.querySelector('ul')
$('<li>').addClass('li-6').text('我是li-6').appendTo(ulEl)
```


# 二、jQuery的DOM操作

## 2.1 移除/克隆/替换
**empty()**:删除匹配元素集的**所有子节点，自身不会删除。**

**remove()、.remove( `[selector]`)**

* 删除匹配的元素集，**自身也会删除**。
	* selector参数:字符串类型选择器。筛选匹配元素集的元素来删除

**.replaceAll(target)**:用匹配到的元素集替换每个目标元素。

**.replaceWidth(newContent)、.replaceWidth( function )**

* 用新内容替换匹配元素集中的每个元素，并返回被移除的元素集。
	* newConten参数的类型:HTMLstring，DOM element, array of DOM elements, or iQuery obiect

```js
//创建元素,并替换匹配到的元素
$('<span>').text('我是span').replaceAll('ul li')
  
//匹配元素，并替换匹配元素
var $span = $('<span>').text('我是span')
$('ul li').replaceWith( $span )
```

**.clone()、.clone( withDataAndEvents )**

* 对匹配的元素集执行**深度复制**，底层是调用了**elem.cloneNode( true )**来复制元素
	* withDataAndEvents参数:布尔值，是否**复制该元素**的事件处理程序和数据，默认值为false。

```js
 $('<li>')
 .addClass('li-6')
 .text('li-6')
 .data({
  name: "axl",
  age: 18
 })
 .click(function() {
  console.log("li-6发生了点击")
 })
 .clone()
 //.clone(true)
 .appendTo('ul')
 //clone参数默认flase，存在data自定义属性和click点击事件。点击li-6的时候不会进行打印。
 //clone参数为true的时候机会把data数据和click点击事件一并进行拷贝。点击li-6就会进行打印
	 //true的时候，jQuery对象也会进行缓存
```

```js
console.log("%O", $('.li-6').get(0))
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17384816740007i5m14.png)



