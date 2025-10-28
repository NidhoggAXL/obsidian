# 一、Map基本使用
另外一个新增的数据结构是Map，用于**存储映射关系**，

但是我们可能会想，在之前我们可以**使用对象来存储映射关系，他们有什么区别**呢?

* 事实上我们对象存储映射关系只能用**字符串(ES6新增了Symbol)作为属性名(key)**

```js
<script>
  const obj1 = {name: "axl"}
  const obj2 = {height: 19.8}
  const bar = {
    [obj1]: "hhh",
    age: 18,
    [obj2]: "www"
  }
  console.log(bar)
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17321045930001gifa3.png)

> 虽然看起来是可以用对象作为属性名的，其实**本质还是把对象隐式转换为`[[Object Object]]`的字符串**。**并且那对象作为属性名还会进行覆盖**（obj1）这个就是被覆盖了。

* 某些情况下我们可能希望通过**其他类型作为key，比如对象**，这个时候**会自动将对象转成字符串来作为key;**

使用map：

```js
<script>
  const obj1 = {name: "axl"}
  const obj2 = {height: 19.8}
  const bar = new Map()
  bar.set(obj1, "haha")
  bar.set(obj2, "hehe")
  console.log(bar)
  //Map(2) {{…} => 'haha', {…} => 'hehe'}
</script>
```

# 二、Map常见的属性和方法
Map常见的属性： 

* size：返回Map中元素的个数； 

Map常见的方法： 

* set(key, value)：在Map中添加key、value，并且返回整个Map对象； 
* get(key)：根据key获取Map中的value； 
* has(key)：判断是否包括某一个key，返回Boolean类型； 
* delete(key)：根据key删除一个键值对，返回Boolean类型； 
* clear()：清空所有的元素； 
* **forEach(callback, [, thisArg])**：通过forEach遍历Map； 


Map也可以通过for of进行遍历,不过遍历打印的解构不同。

```js
<script>
  const obj1 = {name: "axl"}
  const obj2 = {height: 19.8}
  const bar = new Map()
  bar.set(obj1, "haha")
  bar.set(obj2, "hehe")
  for( const item of bar) {
    console.log(item)
    //[{…}, 'haha']
    //[{…}, 'hehe']
  
    //想要得到value值使用解构
    const [key, value] = item
    console.log(key, value)
    //{name: 'axl'} 'haha'
    //{height: 19.8} 'hehe'
  }
</script>
```

# 三、WeakMap的使用

和Map类型的另外一个数据结构称之为**WeakMap**，也是**以键值对的形式存在的**。 

那么和Map有什么区别呢？ 

* 区别一：WeakMap的key**只能使用对象**，不接受其他的类型作为key； 
* 区别二：WeakMap的**key对象的引用是弱引用**，如果没有其他引用引用这个对象，那么GC可以回收该对象；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732105954000iokxju.png)

**WeakMap常见的方法有四个：** 

* set(key, value)：在Map中添加key、value，并且返回整个Map对象； 
* get(key)：根据key获取Map中的value； 
* has(key)：判断是否包括某一个key，返回Boolean类型； 
* delete(key)：根据key删除一个键值对，返回Boolean类型；

# 四、WeakMap应用

注意：WeakMap也是不能遍历的 

* 没有forEach方法，也不支持通过for of的方式进行遍历；

那么我们的WeakMap有什么作用呢？（后续专门讲解）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732106042000sj8be3.png)

