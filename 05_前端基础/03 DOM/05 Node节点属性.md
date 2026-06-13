目前，我们已经可以获取到节点了，接下来我们来看一下节点中有哪些常见的属性:

* 当然，不同的节点类型有可能有不同的属性;
* 这里我们主要讨论**节点共有的属性**

# 一、nodeType

* nodeType 属性提供了一种获取**节点类型**的方法;
* 它有一个**数值型值(numeric value);**

```js
<body>
  <!-- 我是注释 -->
  我是文本
  <div class="box">我是box</div>
  <script>
    var bodyNode = document.body.childNodes
    var shNode = bodyNode[1]
    var textNode = bodyNode[2]
    var divNode = bodyNode[3]
    console.log(shNode.nodeType, textNode.nodeType, divNode.nodeType)
    //8 3 1
  </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728224952000fukvyp.png)

其他类型可以査看MDN文档: https://developer.mozilla.org/zh-CN/docs/Web/AP!/Node/nodeType

# 二、nodeName、tagName
**nodeName**:获取node节点的名字:

**tagName**:获取元素的标签名词;

```js
<body>
  <!-- 我是注释 -->
  我是文本
  <div class="box">我是box</div>
  <script>
    var bodyNode = document.body.childNodes
    var shNode = bodyNode[1]
    var textNode = bodyNode[2]
    var divNode = bodyNode[3]
    console.log(shNode.nodeName, textNode.nodeName, divNode.nodeName)
    //#comment #text DIV
    console.log(shNode.tagName, textNode.tagName, divNode.tagName)
    //undefined undefined 'DIV'
  </script>
</body>
```

**tagName和 nodeName 之间有什么不同呢?**

* **tagName** 属性仅适用于 Element 节点;
* **nodeName** 是为任意 Node 定义的:
	* 对于元素，它的意义与 tagName相同，所以使用哪一个都是可以的;
	* 对于其他节点类型(text，comment等)，它拥有一个对应节点类型的字符串;


# 三、innerHTML、outerHTML、textContent

**innerHTML 属性**

* 将元素中的 HTML 获取为字符串形式;
* 设置元素中的内容

获取：

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    console.log(divNode.innerHTML)
    /*<h1>我是标题</h1>
    <p>我是内容</p>*/
  </script>
</body>
```

设置内容：

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    console.log(divNode.innerHTML)
    divNode.innerHTML = "我是修改的哈哈哈"
  </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728226261000fcmfz6.png)


**outerHTML属性**

* 包含了元素的完整 HTML
* innerHTML加上元素本身一样;

获取

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    console.log(divNode.outerHTML)
    /*<div class="box">
      <h1>我是标题</h1>
      <p>我是内容</p>
    </div>*/
  </script>
</body>
```

设置内容：

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    divNode.outerHTML = "我是outerHTML修改后的"
  </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/172822652400039ff84.png)


**textContent 属性**

* 仅仅获取元素中的文本内容

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    console.log(divNode.textContent)
    /*我是标题
    我是内容*/
  </script>
</body>
```

设置：

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    divNode.textContent = "我是textContent修改后的"
  </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728226680000pzphqd.png)

**innerHTML和textContent的区别:**

* 使用 innerHTML，我们将其 **“作为 HTML”插入**，带有所有 HTML 标签。
* 使用 textContent，我们将其 **“作为文本”插入**，所有符号(symbol)均按字面意义处理

innerHTML：

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    divNode.innerHTML = "<h3>我是h3元素</h3>"
  </script>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17282267900008hi4ms.png)

textContent：

```js
<body>
  <div class="box">
    <h1>我是标题</h1>
    <p>我是内容</p>
  </div>
  <script>
    var bodyNode = document.body.childNodes
    var divNode = bodyNode[1]
    divNode.textContent = "<h3>我是h3元素</h3>"
  </script>
</body>
```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728226812000ipoquo.png)

# 四、nodeValue

nodeValue/data

* 用于获取**Document节点**的文本内容
* **Element节点**的内容为 null

```html
<body>
  coderaxl
  <!-- 注释内容 -->
  <script>
    var text = document.body.firstChild
    console.log(text.nodeValue)//coderaxl
  
    var comment = text.nextSibling
    console.log(comment.nodeValue)//注释内容
  </script>
</body>
```


# 五、节点的其他属性
**hidden属性**:也是一个全局属性，可以用于设置元素隐藏。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17283866580000nlqgy.png)

> 其本质是添加了hidden属性会把设置这个元素 display: none;

hidden 属性的使用：

```js
<body>
  <button class="btn">切换</button>
  <div class="box">我是div元素</div>

  <script>
    var divEl = document.querySelector(".box")
    var btnEl = document.querySelector(".btn")
    btnEl.onclick = function() {
      divEl.hidden = !divEl.hidden
    }
  </script>
</body>
```

如果点击按钮，就会对div元素进行隐藏和显示的转换。


**DOM 元素还有其他属性:**

 value
 
* `<input>、<select>、<textarea>`
* `(HTMLInputElement, HTMLSelectElement...)` 的value.


 href
 
* `<a href=".">(HTMLAnchorElement)的 href.`

id

* 所有元素(HTMLElement)的“id”特性(attribute)的值。