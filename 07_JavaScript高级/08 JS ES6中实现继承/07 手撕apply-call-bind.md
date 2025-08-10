# 一、apply-call

# 1.1 基础理论

如果给一个字符串使用 Object() 内部的对象结构是什么样子： 

```js
console.log(Object("abc")[0]);//a

let main = {
  0: 'a',
  1: 'b',
  d: 'd'
}
console.log(main[0]);//a
console.log(main.d);//a
// console.log(main.0);这样会报错，是错误的使用

```

> [!inof] 如果给一个字符串使用 Object() 的话就会变成上门 mian 变量的样子,只是我添加了一个 d 的属性,来进行测试.
> 只有 Object(String) 语法创建出来的 **对象** ,才可以使用 **`main[0]`** 的语法,且不可以使用对象的正常语法,除非在 main 对象里面添加**如上面 d 一样的正常属性,才可以正常的访问你正常编写的属性**.

## 2.1 代码演示

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

核心方法 `myexe`（实现 `this` 绑定的关键）

```js
Function.prototype.myexe = function(thisArg, otherArgs) {
  // 处理 thisArg：null/undefined 转为 window，其他值转为对象
  thisArg = (thisArg === null || thisArg === undefined) ? window : Object(thisArg)
  
  // 在 thisArg 上创建临时方法 fn
  Object.defineProperty(thisArg, "fn", {
    enumerable: false,   // 不可枚举
    configurable: true,  // 可配置（后续可删除）
    value: this          // 关键！这里的 this 指向调用 myexe 的函数
  })
  
  // 通过 thisArg 调用 fn（实现 this 绑定）
  thisArg.fn(...otherArgs)
  
  // 删除临时方法
  delete thisArg.fn
}
```

**`this` 指向分析**：

1. 当 `myexe` 被调用时（如 `foo.myexe(...)`）：
    
    - **函数内的 `this`**：指向调用者 `foo` 函数对象
        
    - `value: this`：将 `foo` 函数存储到 `thisArg.fn`
        
2. 当执行 `thisArg.fn(...)` 时：
    
    - **函数调用方式**：作为 `thisArg` 对象的方法调用
        
    - **`foo` 内部的 `this`**：指向 `thisArg` 对象（隐式绑定规则）
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
      value: this
      //this是foo
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


