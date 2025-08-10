# 一、认识事件（Event)
Web页面经常需要和用户之间进行交互，而交互的过程中我们可能想要捕捉这个交互的过程:

* 比如用户点击了某个按钮、用户在输入框里面输入了某个文本、用户鼠标经过了某个位置
* 浏览器需要搭建一条JavaScript代码和事件之间的桥梁,
* 当某个事件发生时，让JavaScript执行某个函数，所以我们需要针对事件编写处理程序(handler)

**原生事件监听方法:**

* 事件监听方式一:在script中直接监听(很少使用)
* 事件监听方式二:DOM属性，通过元素的on来监听事件。
* 事件监听方式三:通过EventTarget中的addEventListener来监听。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738482641000l5jlxs.png)

> onclick方式的话，如果后面在继续这个元素上面编写这个方法的话，会覆盖原来元素上面编写的onclik

**jQuery事件监听方法:**

* 事件监听方式一:直接**调用jQuery对象中的事件处理函数**来监听，例如:click，mouseenter..
* 事件监听方式二:调用jQuery对象中的**on函数**来监听，使用off函数来取消监听。

> 底层是调用原生的 addEventListener 方法

```js
//on方式
$('ul').on('click', function() {
 console.log('click1')
})
  
//简写方式click
$('ul').click(function() {
 console.log('click2')
})
```

> 这种方式的编写，并**不会进行覆盖**，当点击ul的时候会进行两次打印

## 1.1 off函数取消监听
```js
//on方式
$('ul').on('click', function() {
 console.log('click1')
})
  
//简写方式click
$('ul').click(function() {
 console.log('click2')
})

//监听按钮，进行ul的事件监听取消
$('button').click(function() {
 $('ul').off()//取消所有的事件监听
 // $('ul').off('click')//取消所有的点击事件
})
```


## 1.2 自动触发事件
自动触发事件，用与一些测试当中，模拟用户点击。trigger-触发器

```js
$('ul').trigger('click')
```

当进行网页的加载的时候，已加载完成就会进行ul的自行点击事件。


# 二、click和on的区别
click和on的区别:

* click是on的**简写**。它们重复监听，**不会出现覆盖情况，都支持事件委托**，底层用的是addEventListener。
* 如果 on 没有使用 selector 的话，那么和使用click是一样的。
* on 函数可以**接受一个 selector 参数，用于筛选 可触发事件 的后代元素**
* on 函数支持给事件**添加命名空间**。

```js
//click.axl点后面的axl就是命名空间
$('ul').on('click.axl', function() {})
  
//selector选择器
$('ul').on('click', '字符串类型选择器', function() {})
```

> **命名空间的作用**：如果ul元素上面有两个点击事件，可以通过命名空间改变点击名字，这样就不会通过`$('ul').off('click')`全部删除点击事件
> 
> **selector参数的作用**：在后面的事件委托会用到


# 三、click和on中this指向
click和on的this指向:

* this都是指向原生的DOM Element

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17384856170003ytxih.png)

# 四、jQuery事件冒泡
我们会发现默认情况下事件是从最内层(如下图span)向外依次传递的顺序，这个顺序我们称之为事件冒泡(Event Bubble)

事实上，还有另外一种监听事件流的方式就是从外层到内层(如:body ->span)，这种称之为事件捕获(Event Capture)

为什么会产生两种不同的处理流呢?

* 这是因为早期在浏览器开发时，不管是IE还是Netscape公司都发现了这个问题，
* 但是他们采用了完全相反的事件流来对事件进行了传递，
* IE<9仅采用了事件冒泡的方式，Netscape采用了事件捕获的方式
* IE9+和现在所有主流浏览器都已支持这两种方式。

**jQuery为了更好的兼容IE浏览器，底层并没有实现事件捕获，**

# 五、jQuery事件对象
jQuery事件系统的规范是**根据W3C的标准**来制定**jQuery事件对象**。原身事件对象的大多数属性都被**复制到新的jQuery事件对象上**。如，以下原生的事件属性被复制到jQuery事件对象中:

* altKey, clientX, clientY, currentTarget, data, detail, key, keyCode, offsetX, offsetY, originalTarget, pageX, pageYrelatedTarget,screenX,screenY, target,

jQuery事件对象通用的属性(以下属性已实现跨浏览器的兼容

* target、relatedTarget、pageX、pageY、which、 metaKey

jQuery事件对象常用的方法

* **preventDefault()**:取消事件的默认行为(例如，a标签、表单事件等)
* **stopPropagation()**:阻止事件的进一步传递(例如，事件冒泡)

要访问其它事件的属性，可以使用 **event.originalEvent** 获取原生对象


1. 获取事件对象

```js
//获取ul的原生的事件对象
var ulEl = document.querySelector('ul')
ulEl.addEventListener('click', function(event) {
 console.log(event)
})
  
//获取ul的jQuery事件对象
$('ul').on('click', function($event) {
 console.log($event)
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738487604000uku89t.png)

2. jQuery事件对象的方法

```js
$('a').click(function($event) {
 //组织a元素的默认点击跳转
 $event.preventDefault()
})
  
$('.content').click(function($event) {
 //阻止事件的冒泡
 $event.stopPropagation()
})
```


# 六、jQuery事件委托
事件冒泡在某种情况下可以帮助我们实现强大的事件处理模式-事件委托模式(也是一种设计模式)

那么这个模式是怎么样的呢?

* 因为当子元素被点击时，父元素可以通过冒泡监听到子元素的点击
* 并且可以通过event.target获取到当前监听事件的元素(event.currentTarget获取到的是处理事件的元素);

案例:一个ul中存放多个li，使用事件委托的模式来监听li中子元素的点击事件。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738499657000ukl559.png)


# 七、jQuery常见的事件
**鼠标事件(Mouse Events)**

* .click(、.dblclick()、.hover()、.mousedown()、.mouseup()
* .mouseenter()、.mouseleave()、.mousemove()
* .mouseover()、.mouseout().contextmenu()、.toggle()

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738499718000fkfn1p.png)

```js
$('ul').hover(function() {
 console.log("鼠标悬浮ul")
}, function() {
 console.log("鼠标离开ul")
})
```

> 可以同时进行悬浮和离开的监听，底层是调用了 mouseenter 和 mouseleave 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738500614000ahyhfq.png)


**键盘事件(Keyboard Events)**

* .keydown().keypress() keyup()

**文档事件(Document Loading Events)**

* load、ready() unload

**表单事件(Form Events)**

* .blur()-失去焦点、.focus()-聚焦 .change() .submit() .select() .input()-输入

```js
   $('input').focus(function() {
    console.log("聚焦事件")
   }).blur(function() {
    console.log("失焦事件")
   }).on('input', function() {
    console.log($('input').val())
    // console.log($(this).val())
   })
```

**浏览器事件(Browser Events)**

* .resize() scroll()

```js
$(window).resize(function() {
	console.log('reseze')
})
```


# 八、jQuery的键盘事件
事件的执行顺序是 keydown()、keypress()、keyup()

* keydown事件先发生;
* keypress发生在文本被输入;
* keyup发生在文本输入完成(抬起、松开);

我们可以通过key和code来区分按下的键:

* code:“按键代码”("KeyA"，"ArrowLeft"等)，特定于键盘上按键的物理位置。
* key：字符("A"，“a"等)，对于非字符(non-character)的按键，通常具有与 code 相同的值。)


# 九、jQuery表单事件
表单事件(Form Events)

* .blur()-元素失去焦点时触发
* .focus()-元素获取焦点时触发
* change()-该事件在表单元素的内容改变时触发`( <input>,<keygen>,<select>,和 <textarea>)`
* .submit()-表单提交时触发
* ……

# 十、jQuery选项卡切换
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738503646000ts6zk2.png)



 