**在元素中的属性叫做attribute，对象中的属性叫做property**

```js
<body>
  <!-- class叫做attribu -->
  <div class="box"></div>
  
  <script>
    //对象中的属性叫做property
    var bar = {
      class: "box"
    }
  </script>
</body>
```

>[!tip] 注意点：
>* 对于**标准的attribute**，会在DOM对象上创建**与其对应的property属性**:
>* 标准的attribute通过点（`.`）就可以获取到属性

```js
<body>
  <input type="checkbox" checked>
  <script>
    var inputEl = document.querySelector("input")
    if (inputEl.checked) {
      console.log(typeof inputEl.checked)//boolea
      console.log("存在checked属性")//存在checked属性
    }
  </script>
</body>
```

> 这样的好处是得到的属性是一个布尔类型，而不是字符串，这样就避免了得到一个空字符不好操作


**在大多数情况下，它们是相互作用的**

* 改变property，通过attribute获取的值，会随着改变;
* 通过attribute操作修改，property的值会随着改变

```js
<body>
  <div class="box" id="01" title="标题"></div>
  <script>
    var divEl = document.querySelector(".box")
  
    divEl.setAttribute("id", "02")//通过attribu修改
    console.log(divEl.id)//02 通过property查看
  
    divEl.title = "不是标题"//通过property修改
    console.log(divEl.getAttribute("title"))//不是标题 通过attribu查看
  </script>
</body>
```

除非特别情况，大多数情况下，设置、获取attribute，推荐使用property的方式:

* 这是因为它默认情况下是**有类型的（boolean）**


