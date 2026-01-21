# 一、set的基本使用
在ES6之前，我们存储数据的结构主要有两种：**数组、对象**。 

* 在ES6中新增了另外两种数据结构：**Set、Map**，以及它们的另外形式WeakSet、WeakMap。

Set是一个新增的数据结构，可以用来保存数据，**类似于数组**，但是和数组的**区别是元素不能重复。** 

* 创建Set我们需要通过**Set构造函数**（暂时没有字面量创建的方式）：

我们可以发现Set中存放的元素**是不会重复（地址重复）的，那么Set有一个非常常用的功能就是**给数组去重。

```html
<script>
  //1.给数组去重
  //1.1 不适用set
  const bar = ["abc", "nba", "mba", "abc"]
  const newBar = []
  for(const item of bar) {
    if(!newBar.includes(item)) {
      newBar.push(item)
    }
  }
  //去重后的数组
  console.log(newBar)
  //(3) ['abc', 'nba', 'mba']

  const arr = ["abc", "nba", "mba", "abc"]
  const newArrSet = new Set(arr)
  console.log(newArrSet)
  //set 去重的效果，是一个set类型，不是数组
  //Set(3) {'abc', 'nba', 'mba'}
  //将set类型转为 数组类型
  const newArr = Array.from(newArrSet)
  console.log(newArr)
  //(3) ['abc', 'nba', 'mba']
</script>
```

# 二、Set常见属性和方法

Set常见的属性:

* size:返回Set中元素的个数;

Set常用的方法:

* **add(value)**:添加某个元素，返回Set对象本身;
* **delete(value)**:从set中删除和这个值相等的元素，返回boolean类型
* **has(value)**:判断set中是否存在某个元素，返回boolean类型;
* **clear():** 清空set中所有的元素，没有返回值;
* **forEach(callback,[, thisArg])**:通过forEach遍历set;

```js
<script>
  const arr = ["mba", "cba", "abc"]
  const arrSet = new Set(arr)
  arrSet.forEach( item => console.log(item) )
  //mba
  //cba
  //abc
</script>
```

**另外Set和Array一样是支持for of的遍历的。**

```js
<script>
  const arr = ["mba", "cba", "abc"]
  const arrSet = new Set(arr)
  for(const item of arrSet) {
    console.log(item)
    //mba
    //cba
    //abc
  }
</script>
```

# 三、WeakSet的使用
## 3.1 强弱引用
强引用就是被根对象开始引用（**默认的引用都是强引用**）

弱引用就是不是从根对象开始的引用

* WeankSet就是一个弱引用
* WeakMap也是一个弱引用

## 3.2 WeakSet基本使用

先来看一下let、arr之间的内存简单图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1732102605000pop7gv.png)

**如果打印的话：**

```js
console.log(arr)
//0: {name: 'abc'}
//1: {name: 'mba'}
//2: {name: 'cba'}
```

> 上面数组里面对obj对象的里面的属性对象引用就是一个强引用，所以当obj为null的时候，属性对象还是存在的

和Set类似的另外一个数据结构称之为WeakSet，也是内部元素不能重复的数据结构。

那么和Set有什么区别呢?

* 区别一:WeakSet中**只能存放对象类型**，**不能存放基本数据类型**，
* 区别二:WeakSet对**元素的引用是弱引用**，如果没有其他引用对某个对象进行引用，那么[[02 垃圾回收机制算法#一、JavaScript的垃圾回收|GC]]可以对该对象进行回收;

WeakSet常见的方法:

* **add(value)**:添加某个元素，返回WeakSet对象本身;
* **delete(value)**:从WeakSet中删除和这个值相等的元素，返回boolean类型，
* **has(value)**:判断WeakSet中是否存在某个元素，返回boolean类型;

# 四、WeakSet的应用

**注意**：WeakSet不能遍历 

* 因为**WeakSet只是对对象的弱引用**，如果我们遍历获取到其中的元素，那么有可能造成对象不能正常的销毁。 
* 所以**存储到WeakSet中的对象是没办法获取**的；

那么这个东西有什么用呢？ 

* 事实上这个问题并不好回答，我们来使用一个Stack Overflow上的答案；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17321039260005o1dtv.png)

