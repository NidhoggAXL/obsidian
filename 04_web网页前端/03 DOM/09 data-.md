当我们在想使用自己定义的[[06 元素的特性attribute|attribute]]的时候会使用getAttribute来获取这个属性

那么如果不使用getAttribute的时候就可以使用 `data-*`来自定义属性

```js
<div class="box" data-height="18.8" data-age="18"></div>

<script>
  var divEl = document.querySelector(".box")
  
  //获取使用 data- 设置（set）的所有attribute
  console.log(divEl.dataset)
  //OMStringMap {height: '18.8', age: '18'}
  
  //获取 data- 设置的ttribute值
  console.log(divEl.dataset.height)//18.8
</script>
```

> [!tip] 开发中运用
> 在小程序的开发中我们会使用到这个
