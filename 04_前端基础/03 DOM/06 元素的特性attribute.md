# 一、attribute的分类
**标准的attribute**:某些attribute属性是标准的，比如id、class、href、type、value等;

**非标准的attribute**:某些attribute属性是自定义的，比如abc、age、height等;

```js
<div class="box" id="#" href="#" abc="avc" age="18"></div>
```

# 三、attribute的操作
对于所有的attribute访问都支持如下的方法:

* elem.hasAttribute(name)- 检查特性是否存在。
* elem.getAttribute(name) - 获取这个特性值。
* elem.setAttribute(name, value)- 设置这个特性值。
* elem.removeAttribute(name) - 移除这个特性,
* attributes:attr对象的集合，具有name、value属性:

```js
<body>
  <div class="box" id="#" href="#" abc="avc" age="18"></div>
  <script>
    var boxEl = document.querySelector(".box")
    for (var attr of boxEl.attributes) {
      console.log(attr.name, attr.value)
      /*
      class box
      id #
      href #
      abc avc
      age 18
      */
    }
  
    console.log(boxEl.hasAttribute("age"))//true
    console.log(boxEl.getAttribute("abc"))//avc
    boxEl.setAttribute("age", "20")
    boxEl.removeAttribute("abc")
  
    for (var attr of boxEl.attributes) {
      console.log(attr.name, attr.value)
      /*
      class box
      id #
      href #
      age 20
      */
    }
  </script>
</body>
```

attribute具备以下特征:

* 它们的名字是**大小写不敏感**的(id 与 ID 相同)
* 它们的值**总是字符串类型**的。

```js
<body>
  <input type="checkbox" checked>
  <script>
  var inputEl = document.querySelector("input")
  console.log(inputEl.getAttribute("checked"))
  </script>
</body>
```

> 会发现我拿到的是一个空的字符串，但是我们在使用的时候是希望给我们返回一个布尔类型的更好一点，方便我们进行操作

