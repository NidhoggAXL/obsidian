# 一、let、const基本使用
在ES5中我们声明变量都是使用的var关键字，从ES6开始新增了两个关键字可以声明变量:let、const

* let、const在其他编程语言中都是有的，所以也并不是新鲜的关键字;
* 但是let、const确确实实给JavaScript带来一些不一样的东西;

let关键字:

* 从直观的角度来说，**let和var是没有太大的区别的，都是用于声明一个变量;**

const关键字:

* const关键字是constant的单词的缩写，表示常量、衡量的意思;
* 它表示**保存的数据一旦被赋值，就不能被修改;**
* 但是**如果赋值的是引用类型，那么可以通过引用找到对应的对象，修改对象**的内容:

```js
<script>
  const obj = {
    name: "axl"
  }
  obj.name = "mba"
  console.log(obj)
  //{name: 'mba'}
  //但是不可以 obj = {}
</script>
```

> [!tip] 注意:
> 另外let、const不允许重复声明变量;

```js
let info = ""
//不可以通过任何形式在声明 info
```

# 二、let、const作用域提升
let、const和var的另一个重要区别是作用域提升:

* var声明的变量是会进行作用域提升的;
* 但是如果我们使用let声明的变量，在声明之前访问会报错;

```js
<script>
  console.log(info)
  //Uncaught ReferenceError: Cannot access 'info' before initialization
  //未发现引用错误:无法在初始化前访问“info”
  let info = "axl"
</script>
```

那么是不是意味着info变量只有在代码执行阶段才会创建的呢?

* 事实上并不是这样的，我们可以看一下ECMA262对let和const的描述;
* 这些变量会被创建在包含他们的词法环境被实例化时，但是是不可以访问它们的，直到词法绑定被求值:

> **总结就是**：它在没有进行实例化（初始化）的时候（执行上下文的词法环境创建出来的时候）**已经被创建出来了（和var一样），只是这里不可以提前进行访问**

那么let、const到底有没有作用域提升呢？

> [!tip] 自我理解
> **作用域提升**:在声明变量的作用域中，如果这个变量可以在声明之前被访问，那么我们可以称之为作用域提升
> **在这里**，它虽然被创建出来了，但是不能被访问，我认为不能称之为作用域提升;

**那么自我的观点是**：let、const没有进行作用域提升，但是会在解析阶段被创建出来

# 三、暂时性死区（TDZ）
在let、const定义的标识符真正执行到声明的代码之前，是不能被访问的

* 从块作用域的顶部一直到变量声明完成之前，这个变量处在暂时性死区(TDZ，temporwl dead zone)
* 这个名字是JS社区起的名字，**并没有官方的叫法**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731851057000ye6495.png)

* 使用术语“temporal”是因为区域取决于**执行顺序(时间)，而不是编写代码的位置;**

```js
<script>
  function foo() {
    console.log(message)
  }
  let message = "axl"
  foo()//axl
</script>
```

> foo调用的执行里面代码的时候，message已经进行了实例化。

* 智时性死区形成之后，在该区域内这个标识符不能访间

```js
<script>
  function foo() {
    console.log(message)
    let message = "mba"
  }
  let message = "axl"
  foo()//Cannot access 'message' before initialization
</script>
```


# 四、Window对象添加属性
我们知道，在全局通过var来声明一个变量，事实上会在window上添加一个属性:

* 但是let、const是不会给window上添加任何属性的。

那么我们可能会想这个变量是保存在哪里呢?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17318517450000usqw8.png)

> 全局环境记录在逻辑上是单个记录，但它被指定为封装,对象环境记录和声明性环境记录。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1731851817000qxg4bk.png)

> [!tip] 总结就是：
> let、const、var声明的变量都保存在 Global Environment Records（全局环境记录）中。
> * var 保存在全局环境记录的`[[ObjectRecord]]`就是 global object（全局对象-Window）
> * let、const在全局环境记录的`[[DeclarativeRecord]]`(声明环境记录)



