# 一、JavaScript动态修改样式
有时候我们会通过JavaScript来动态修改样式，这个时候我们有两个选择:

* 选择一:在CSS中编写好对应的样式，**动态的添加class;**
* 选择二:动态的**修改style属性**;

开发中如何选择呢?

* 在大多数情况下，如果可以动态修改class完成某个功能，**更推荐使用动态class**
* 如果对于某些情况，无法通过动态修改class(比如**精准修改某个css属性的值**)，那么就可以**修改style属性**

比如：不断点击的时候增加元素的宽度，这个时候通过CSS就修改不了，就要使用style属性

```js
<body>
  <div class="box" style="background-color: red; width: 100px;">
    我是div元素
  </div>
  <script>
    var divEl = document.querySelector(".box")
    var count = 1
    divEl.onclick = function() {
      divEl.style.width =100 * count++ + "px"
    }
  </script>
</body>
```

# 二、元素的className和classList
元素的class attribute，对应的property并非叫class，而是className:

* 这是因为JavaScript早期是不允许使用class这种关键字来作为对象的属性，所以DOM规范使用了className
* 虽然现在JavaScript已经没有这样的限制，但是**并不推荐**，并且依然在使用className这个名称;

我们可以对className进行赋值，它会替换整个类中的字符串

```js
var boxEl = document.querySelector(".box")
boxEl.className = "why abc"
```


如果我们需要**添加或者移除单个的class**，那么可以使用classList属性

elem.classList 是一个特殊的对象:

* elem.classList.add(class):添加一个类
* elem.classList.remove(class):添加/移除类。
* elem.classList.toggle(class):如果类不存在就添加类，存在就移除它
* elem.classList.contains(class):检查给定类，返回 true/false。

**classList是可迭代对象，可以通过for of进行遍历。**

# 三、style属性
如果需要单独修改某一个CSS属性，那么可以通过style来操作:

* 对于多词(multi-word)属性，使用**驼峰式 camelcase**

```js
boxEl.style.width = "100px"
boxEl.style.height ="50px'"
boxEl.style.backgroundColor ="red"
```


如果我们将值设置为空字符串那么会使用CSS的默认样式

```js
boxEl.style.display = ""
```

多个样式的写法，我们需要使用**cssText属性**:

* 不推荐这种用法，因为它会替换整个字符串;

```js
boxEl.style.cssText = `
	width: 100px;
	height: 100px;
	background-color:red;`
```

# 四、元素style的读取

如果我们需要读取样式:

* 对于内联样式，是可以通过`style.*`的方式读取到的;
* 对于style、css文件中的样式，是读取不到的

```js
<style>
	.box {
	  font-size: 30px;
	}
</style>

<body>
  <div class="box" style="background-color: red; color: orange;">
    我是div元素
  </div>
  <script>
    var divEl = document.querySelector(".box")
    console.log(divEl.style.backgroundColor)//red
    console.log(divEl.style.fontSize)//空
  </script>
</body>
```


这个时候，我们可以通过getComputedStyle的全局函数来实现:

* get - 得到
* computed - 计算

```js
console.log(getcomputedstyle(boxE1).width)
console.log(getcomputedstyle(boxEl).height)
console.log(getcomputedstyle(boxE1).backgroundColor)
```


