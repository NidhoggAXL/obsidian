# 一、apply-call
```js
<script>
  function foo(name, age) {
    console.log(this, name, age)
  }
  
  Function.prototype.myexe = function(thisArg, otherArgs) {
    thisArg = (thisArg === null || thisArg === undefined)? window : Object(thisArg)
  
    Object.defineProperty(thisArg, "fn", {
      enumerable: false,
      configurable: true,
      value: this
      //这里的this是foo
      //把foo绑定到 thisArg
    })
    thisArg.fn(...otherArgs)
    //thisArg对象上面调用fn函数里面的this，是一个隐式绑定
    //这个时候this指向这个对象
    delete thisArg.fn
    //foo中this的绑定发生了改变
  }

  Function.prototype.myApply = function(thisArg, otherArgs) {
    this.myexe(thisArg, otherArgs)
    //foo.myexe()
  }
  
  Function.prototype.myCall = function(thisArg, ...otherArgs) {
    this.myexe(thisArg, otherArgs)
    //foo.myexe()
  }
  
  foo.myApply("abc", ["axl", 18])
  foo.call("mba", "lala", 19)
</script>
```

# 二、bind
```js
<script>
  function foo(name, age, height, adress) {
    console.log(this, name, age, height, adress)
  }
  
  Function.prototype.myBind = function(thisArg, ...otherArgs) {
    // console.log(this)//this是foo
    thisArg = (thisArg === null || thisArg === undefined)? window : Object(thisArg)
    Object.defineProperty(thisArg, "fn", {
      enumerable: false,
      configurable: true,
      writable: false,
      value: this//value读取属性时放回该值（foo）
      //把foo绑定到thisArg对象上
    })
    return (...newotherArgs) => {
      // this()
      //箭头函数没有this，会向上层作用域查找

      //对象调用fn函数，隐式绑定this指向调用的对象
      // thisArg.fn()

      //合并参数
      var allArgs = newotherArgs.concat(otherArgs)
      //也可以
      // var allArgs = [...newotherArgs, ...otherArgs]
      thisArg.fn(...allArgs)
    }
  }
  
  var newFoo = foo.myBind("mba", "axl", 18)
  newFoo(19.8, "云南")
  //多个参数多次传入
</script>
```


