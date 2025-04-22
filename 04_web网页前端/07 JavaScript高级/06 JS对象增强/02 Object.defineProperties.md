Object.defineProperties()方法直接在一个对象上定义 多个 新的属性或修改现有属性，并且返回该对象。

```js
<script>
  var obj = {
    name: "axl",
    age: 18,
    address: "曲靖"
  }
  
  Object.defineProperties(obj, {
    name: {
      writable: false,
      value: "mba"
    },
    age: {
      get: function() {
        return this.address
      }
    }
  })
  
  console.log(obj.name)//mba
  console.log(obj.age)//曲靖
</script>
```
