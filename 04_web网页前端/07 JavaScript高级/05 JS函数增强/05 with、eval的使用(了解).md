# 一、with
with语句 扩展一个语句的作用域链

```js
  <script>
    var obj = {
      message: "hello"
    }
  
    with(obj) {
      //扩展了作用域到 obj
      console.log(message)//hello
    }

    console.log(message)//message is not defined
  </script>
```


> [!tip] 注意事项：
> 不建议使用with语句，因为它可能是混淆错误和兼容性问题的根源。

# 二、eval函数

内建函数 eval 允许执行一个代码字符串

* eval是一个**特殊的函数**，它可以**将传入的字符串当做JavaScript代码来运行**
* eval会将**最后一句执行语句的结果，作为返回值;**

```js
<script>
  var statement = `var message = "hello"; console.log(message)`
  
  var result = eval(statement)//hello
  
  //return console.log() 是一个undefined
  console.log(result)//undefined
</script>
```

> [!tip] 不建议在开发中使用eval:
> * eval代码的**可读性非常的差**(代码的可读性是高质量代码的重要原则)
> * eval是一个字符串，那么有可能在执行的过程中被刻意篡改，那么可能会造成被攻击的风险
> * eval的执行**必须经过JavaScript解释器，不能被JavaScript引擎优化;**

