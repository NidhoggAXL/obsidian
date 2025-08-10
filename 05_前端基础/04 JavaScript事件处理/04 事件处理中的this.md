在函数中，我们也可以通过this来获取当前的发生元素:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734165128000xbqn2b.png)


这是因为在浏览器内部，调用event handler是绑定到**当前的currentTarget上的**

```js
<button class="btn">我是按钮</button>

<script>
  var btnEl = document.querySelector(".btn")
  btnEl.onclick = function(event) {
    console.log(this)
    console.log(event.target)
    console.log(event.currentTarget)
    console.log(btnEl)
    console.log(this === btnEl)
  }
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734165616000hjk4ex.png)
