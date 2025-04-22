# 一、CommonJS规范和Node关系
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174377017300082pbm6.png)

# 二、模块化案例

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743770227000gb538s.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743770632000fvq7fu.png)

在 main 中使用导入的数据的时候，都需要 utls 的前缀会比较麻烦，这个时候我们就可以使用[[05 解构Destructuring|解构]]来简化代码：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174377085300035n68a.png)

# 三、exports和require的本质

require 的本质是把 exports 进行地址的引用赋值操作，就是把 exports 对象的地址直接复制给 require ， 这样 require 和 exports 都是指向同一个对象。

![[exports和require的本质|600]]


上面模块化完成了什么操作呢?理解下面这句话，Node中的模块化一目了然

* 意味着main中的 **bar变量等于exports对象**
* 也就是require通过各种查找方式，最终找到了exports这个对象
* 并且将这个exports对象赋值给了bar变量
* bar变量就是exports对象了

```js
let name = 'coderwhy'

// 进行一个导出创建exports对象
exports.name = name
  
// 判断导出的 exports.name 地址是否等于 let 定义的 name
console.log(name === exports.name)//true
  
// 重新定义了 export.name 地址就会发生改变
exports.name = "axl"
  
//export.name地址发生改变对 let name 没有影响
console.log(name)//coderwhy
  
//export.name地址发生改变就和 let name 地址不同
console.log(name === exports.name)//false
```

> 只是 exports.name 地址发生了改变，可以理解为指向的**地址发生改变**，**但是 exports 地址没有发生改变，里面没有进行重新定义的数据也不会发生改变。**

```js
let name = 'axl'
let age = 18
  
exports.name = name
exports.age = age
  
exports.name = 'aoao'
//对exports里面的name重新定义了，改变了地址
console.log(name === exports.name)//false
  
// 没有重新定义age，所以地址没有发生改变
console.log(age === exports.age)//true
```

# 四、module.exports导出
但是Node中我们经常导出东西的时候，又是通过module.exports导出的：

module.exports和exports有什么关系或者区别呢？

我们追根溯源，通过维基百科中对CommonJS规范的解析： 

* CommonJS中是没有**module.exports**的概念的； 
* 但是为了实现模块的导出，Node中使用的是**Module的类，每一个模块都是Module的一个实例，也就是module；** 
* 所以在Node中真正用于导出的其实**根本不是exports**，而是**module.exports**； 
* 因为**module才是导出的真正实现者**；


但是，为什么exports也可以导出呢？ 

* 这是因为module对象的exports属性是exports对象的一个引用；

![[module.exports的实质|600]]


> [!tip] 那么肯定会产生怀疑，Node也支持CommonJS，那么已经有一个expots为还要设置一个module.exports呢？
> 这是因为在导出的时候Node会查询 module.exports ，通过 exports 也可以导出，是因为 module.exports 和 exports 是同一个引用，
**如果改变 exports 的引用地址的话就不可以进行导出了。**![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743837746000h69zrx.png)
**但是改变 modele.exports 的地址引用，还是可以进行导入的（Node是查看 module.exports)**![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743837928000mv8b3o.png)

# 五、CommonJS缺点
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17438436360000oz6yc.png)

[[04 AMD和CMD(了解)]]]