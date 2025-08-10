# 一、Symbol的基本使用
Symbol是什么呢?Symbol是ES6中新增的一个基本数据类型，翻译为符号。

那么为什么需要Symbol呢?

* 在ES6之前，对象的属性名都是字符串形式，那么很容易造成**属性名的冲突**
* 比如原来有一个对象，我们希望在其中**添加一个新的属性和值**，但是我们在不确定它原来内部有什么内容的情况下，**很容易造成冲突，从而覆盖掉它内部的某个属性;**
* 比如我们前面在讲apply、call、bind实现时，我们有给其中**添加一个fn属性**，那么如果它内部原来已经有了fn属性了呢?
* 比如开发中我们使用[[02 extends实现继承#四、类的混入mixin（了解）|混入]]，那么混入中出现了同名的属性，必然有一个会被覆盖掉;

Symbol就是为了解决上面的问题，用来生成**一个独一无二的值**。

* Symbol值是通过**Symbol函数**来生成的，生成后可以[[06 ES6对象的增强|作为属性名]]
* 也就是在ES6中，对象的属性名可以使用**字符串**，也可以使用**Symbol值:**

**Symbol即使多次创建值，它们也是不同的**:Symbol函数执行后每次创建出来的值都是独一无二的,


```js
<script>
  const a = Symbol()
  const b = Symbol()
  console.log(a === b)//false
</script>
```

**我们也可以在创建Symbol值的时候传入一个描述description**:这个是ES2019(ES10)新增的特性;

```js
<script>
  //Symbol(description)
  const s1 = Symbol("aaa")
  console.log(s1.description)//aaa
</script>
```

# 二、Symbol作为属性名
属性名的设置方法：

```js
<script>
  const s1 = Symbol()
  const s2 = Symbol()
  
  const obj = {}
  
  //属性名赋值-使用计算属性名
  obj[s1] = "abc"
  obj[s2] = "cba"
  console.log(obj)
  //{Symbol(): 'abc', Symbol(): 'cba'}

  //Object.defineProperty
  Object.defineProperty(obj, s1, {
    enumerable: true,
    configurable: true,
    writable: true,
    value: "ccc"
  })
  console.log(obj)
  //{Symbol(): 'ccc', Symbol(): 'cba'}
  
  //定义字面量直接使用
  const info = {
    [s1]: "aaa",
    [s2]: "bbb"
  }
  console.log(info)
  //{Symbol(): 'aaa', Symbol(): 'bbb'}
</script>
```

获取Symbol和对应的值：

```js
<script>
  const s1 = Symbol()
  const s2 = Symbol()
  
  //定义字面量直接使用
  const info = {
  [s1]: "aaa",
  [s2]: "bbb"
  }
  
  //获取 Symbol
  console.log(Object.getOwnPropertySymbols(info))
  //[Symbol(), Symbol()]
  
  //获取 Symbol 对应的值
  const SymbolValue = Object.getOwnPropertySymbols(info)
  for(let key of SymbolValue) {
    console.log(info[key])
    //aaa  bbb
  }
</script>
```

# 三、相同值的Symbol
前面我们讲Symbol的目的是为了创建一个独一无二的值，那么如果我们现在就是想创建相同的Symbol应该怎么来做呢？ 

```js
<script>
  //相同的scription通过Symbol也不相同
  //通过 Symbol 创建的是独一无二的
  const s1 = Symbol("aaa")
  const s2 = Symbol("aaa")
  console.log(s1 === s2)//false
  
  const s1Key = s1.description
  const s3 = Symbol(s1Key)
  console.log(s1 === s3)//false
</script>
```

* 我们可以使用**Symbol.for**方法来做到这一点； 
* 并且我们可以通过**Symbol.keyFor**方法来获取对应的key；

```js
<script>
  const s1 = Symbol.for("aaa")
  const s2 = Symbol.for("aaa")
  console.log(s1 === s2)//true
  
  console.log(Symbol.keyFor(s1))//aaa
</script>
```

 

