# 一、Proxy基本使用
在ES6中，新增了一个**Proxy类**，这个类从名字就可以看出来，是用于帮助我们创建一个代理的:

* 也就是说，如果我们希望监听一个对象的相关操作，那么我们可以先创建一个代理对象(Proxy对象)
* 之后对该对象的所有操作，都通过代理对象来完成，代理对象可以监听我们想要对原对象进行哪些操作


我们可以将案例用Proxy来实现一次：

* 首先，我们需要**new Proxy对象**，并且传入需要**侦听的对象**以及**一个处理对象**，处理对象可以称之为handler； 
	* `const p = new Proxy(target, handler) `
* 其次，我们之后的操作都是**直接对Proxy的操作**，而不是原有的对象，因为我们需要在handler里面进行侦听；

```js
const obj = {
	name: "axl",
	age: 18
}
const objProxy = new Proxy(obj,{})
```


# 二、Proxy的set和get捕获器
如果我们想要侦听某些具体的操作，那么就可以在handler中添加对应的**捕捉器（Trap）**：

**set和get分别对应的是函数类型；** 

* set函数有四个参数： 
	* target：目标对象（侦听的对象）； 
	* property：将被设置的属性key； 
	* value：新属性值； 
	* receiver：调用的代理对象； 
* get函数有三个参数： 
	* target：目标对象（侦听的对象）； 
	* property：被获取的属性key； 
	* receiver：调用的代理对象；

```js
<script>
  const obj = {
    name: "axl",
    age: 18
  }
  
  const objProxy = new Proxy(obj, {
    set: function(target, property, value) {
      console.log(`监听：${property}发生改变`)
      target[property]= value
    },
    get: function(target, property) {
      console.log(`监听：获取${property}`)
      return target[property]
    }
  })

  console.log(objProxy.name)//监听：获取name  axl
  objProxy.name = "mba"//监听：name发生改变
  
  //对于监听对象改变，被监听对象也会发生改变
  console.log(obj.name)//mba
</script>
```

# 三、Proxy的捕获器

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732193818000a0a1r7.png)

# 四、Proxy的construct和apply
还会看到捕捉器中还有**construct**和**apply**，它们是应用于函数对象的：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17321938790003wbxkv.png)

# 五、Receiver
![[04 Reflect(反射)#四、Receiver的作用|Receiver的作用]]



