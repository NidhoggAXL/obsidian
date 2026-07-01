我们可以通过`[]`来创建一个数组:

* 数组是一种**特殊的对象类型**

```js
var arr = []
console.log(typeof arr)//object
```

# 一、数组的创建方式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17276152980005xyd9h.png)

数组元素从0开始编号(索引index)

* 一些编程语言允许我们使用负数索引来实现这一点，例如 `fruits[-1]`
* Javascript并**不支持这种写法;**

```js
var arr = ["a", "v"]
console.log(arr[-1])//undefined
```

# 二、数组的操作

## 2.1 at查找

数组的基本操作：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17276157470003ic7qi.png)

使用 at 的话就可以使用负数来进行查找

```js
var message = ["abc", "nba", "cba", "123"]

console.log(message.at(-1))//"123"
console.log(message[-1])//undefined
```

## 2.2 push、pop

**开发中基本都是使用方法来操作：** 在数组的尾端添加或删除元素

* push() 在末端添加元素
* pop() 从末端取出一个元素（**每次只能是一个**）

```js
var bar = ["a", "b", "c"]

bar.push("d", "e")
console.log(bar)//['a', 'b', 'c', 'd', 'e']

bar.pop()
bar.pop()
console.log(bar)//['a', 'b', 'c']
```

## 2.3 shift、unshift

在数组的首端添加或删除元素

* shift 取出队列首端的一个元素，整个数组元素向前移动;
* unshift 在首端添加元素，整个其他数组元素向后移动;

```js
var bar = ["a", "b", "c"]

bar.shift()
console.log(bar)//['b', 'c']

bar.unshift("haha", "hehe")
console.log(bar)//['haha', 'hehe', 'b', 'c']
```

>[!tip]
>push/pop 方法运行的比较快，而shift/unshift 比较慢。(这和数组在内存中地址依次排列有关）

## 2.4 splice利器

**arr.splice 方法可以说是处理数组的利器，它可以做所有事情:添加，删除和替换元素。** ^c6d11c

arr.splice的语法结构如下:(**重点使用**) ^ffadfe

`array.splice(start[,deleteCount[,iteml[,item2[,·..]]]])`

* 从**start**索引位置开始，处理数组中的元素;
* **deleteCount**:要删除元素的个数，如果为0或者负数表示不删除;
* **item1,item2,…** 在添加元素时，需要添加的元素;

```js
var bar = ["1", "2", "3"]

// 在索引1的地方增加2个数组元素
bar.splice(1, 0, "abc", "nba")
console.log(bar)//'1', 'abc', 'nba', '2', '3']

// 删除上面增加的数组
bar.splice(1,2)
console.log(bar)//(3) ['1', '2', '3']

// 删除第二个数组元组，并增加2个数组元素
bar.splice(1, 1, "abc", "cba")
console.log(bar)//(4) ['1', 'abc', 'cba', '3']
```

> [!warning] 注意:
> 这个方法会修改原数组

```js
var bar = ["1", "2", "3"]
bar.splice(1, 1)
console.log(bar)//['1', '3']
```

# 三、Length属性

length属性用于获取数组的长度:

* 当我们修改数组的时候，length 属性会自动更新。

length 属性的另一个有意思的点是它是可写的。

* 如果我们手动增加一个大于默认length的数值，那么会增加数组的长度。
* 但是如果我们减少它，数组就会被截断
* 被截断的数组会被内存释放，在增加数组长度是找不到原来截断的数据的

```js
var message = ["abc", "nba", "cba"]

message.length = 2
console.log(message)//['abc', 'nba']

message.length = 3
console.log(message)//['abc', 'nba', empty]
//empty - 空
```

> [!tip]
> 所以，清空数组最简单的方法就是:`arr.length=0;`。


# 四、数组的遍历

数组的遍历有三种方式

```js
var message = ["abc", "nba", "cba"]

//1.普通for循环
for (var i = 0; i < message.length; i++) {
  console.log(message[i])
}
	
//2.for in
for (var index in message) {
  console.log(index, message[index])
}

//3.for of
for (var item of message) {
  console.log(item)
}
```

>[!note] 
>前面两种方法可以拿到索引值

# 五、数组的方法-slice、concat、join

arr.slice 方法(片):用于对数组进行截取(类似于字符串的slice方法)^aaa

* arr.slice`([begin[,end]])`
* 包含begin元素，但是不包含end元素
* **不改变原数组**，而是**创建一个新的数组**

```js
var message = ["abc", "nba", "cba", "123",]

var newMessage = message.slice(1, 3)
console.log(newMessage)//['nba', 'cba']
```

arr.concat方法:创建**一个新数组**，其中包含来自于其他数组和其他项的值。

```js
var a = ["a", "A"]
var b = ["b", "B"]
var c = ["c", "C"]

var newMessage = a.concat(b, c)
console.log(newMessage)
//['a', 'A', 'b', 'B', 'c', 'C']
```

arr.join方法: 将一个**数组的所有元素**连接成一个字符串并返回这个字符串。

```js
var message = ["abc", "nba", "cba", "123"]

console.log(message.join("--"))
//abc--nba--cba--123
```


# 六、数组元素查找

## 6.1 简单数组元素的查找

**arr.indexOf方法::查找某个元素的索引**

`arr.index0f(searchElement[,fromIndex])`

* 从fromIndex开始查找，如果找到返回对应的索引，没有找到返回-1:
	* 默认值为0
* 也有对应的从最后位置开始查找的 lastIndexOf 方法

```js
var message = ["abc", "nba", "cba", "123"]
console.log(message.indexOf("nba"))//1
```

通过 key 直接来进行查找，并且返回的是 **元素所在位置的索引**

**arr.includes方法:判断数组是否包含某个元素**

`arr.includes(valueToFind[,fromIndex])`

* 从索引 from 开始搜索 item，如果找到则返回 true(如果没找到，则返回 false)。

```js
var bar = ["abc", "cba", "nba"]
console.log(bar.includes("cba"))//true
```


**find 和 findIndex 直接查找复杂元素或者复杂元素的索引(ES6名后新增的语法)**

## 6.2 复杂数组元素的查找

普通的方法：

```js
//查找id为101的学生信息
var bar = [
  {id: 100, name: "axl", age: 12},
  {id: 101, name: "coder", age: 20}
]

for (var i = 0; i < bar.length; i++) {
  if (bar[i].id === 101) {
	console.log(bar[i])
	//{id: 101, name: 'coder', age: 20}
  }
}
```

使用 find 方法：

```js
var bar = [
  {id: 100, name: "axl", age: 12},
  {id: 101, name: "coder", age: 20}
]

bar.find(function(item) {
  console.log(item)
  //id: 100, name: 'axl', age: 12}
  //{id: 101, name: 'coder', age: 20}
  if (item.id === 101) {
	console.log(item)
	//{id: 101, name: 'coder', age: 20}
  }
})
```

通过上面可以看出：bar.find() 是一个[[07 回调、高阶、匿名函数|高阶函数]]


**自我实现：**

```js
var bar = [
	{id: 100, name: "axl", age: 12},
	{id: 101, name: "coder", age: 20}
]

//这里的fn就是调用前面的bar
bar.zwFind = function(fn) {
	for(var i = 0; i < this.length; i++) {
		var isFlag = fn(this[i])
		if(isFlag) {
		  return this[i]
		}
	}
}

var student = bar.zwFind(function(item) {
	return item.id === 101
	//放回的是一个表达式，存在就是true，不存在就是false
})

console.log(student)
```


## 6.3 补充forEach
**arr.forEach**：遍历数组，并且让数组中每一个元素都执行一次对应的方法;

```js
var bar = [
  {id: 100, name: "axl", age: 12},
  {id: 101, name: "coder", age: 20}
]

bar.forEach(function(item, index, name) {
  console.log(item, index, name)
})
```

> [!note]
> forEach回调函数里面的参数
> 
> * 第一个参数：每一次遍历的数组值
> * 第二个参数：每一个遍历的索引
> * 第三个参数：遍历的对象数组

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734081394000fvnyex.png)


手撕foreach

```js
//查找id为101的学生信息
var bar = [
  {id: 100, name: "axl", age: 12},
  {id: 101, name: "coder", age: 20}
]

bar.xlForEACH = function(fn) {
  for(var i = 0; i < this.length; i++) {
	fn(this[i], i, this)
  }
}

bar.xlForEACH(function(item, index, names) {
  console.log(item, index, names)
})
```

# 七、数组的排序

sort方法也是一个高阶函数，用于对数组进行排序，并且生成一个排序后的**数组（改变原数组）**:

`arr.sort([compareFunction ])`

* 如果 compareFunction(a,b)小于0，那么a会被排列到 b 前面,
* 如果 compareFunction(a,b)等于0，a和b的相对位置不变
* 如果 compareFunction(a,b)大于0，b会被排列到 a 前面
* 也就是说，谁小谁排在前面;

```js
var num = [4,19,23,31,18]

num.sort(function(item1, item2) {
	return item1 - item2
})

console.log(num)
//[4, 18, 19, 23, 31]
```


**reverse()方法将数组中元素的位置颠倒，并返回该数组：**

```js
console.log(num.reverse())
//[31, 23, 19, 18, 4]
```

# 八、数组的高阶方法

## 8.1 filter-过滤

arr.filter

* filter()方法**创建一个新数组（不会改变原数组）**
* 新数组中只包含每个元素调用函数返回为true的元素;
* 放回的结果如果是 ture 就把值返回到数组里面，会自动进行遍历

```js
var num = [4,19,23,31,18]

var newNum = num.filter(function(item) {
  return item % 2 === 0
})
  
console.log(newNum)
//[4, 18]
```


## 8.2 map-映射

arr.map

* map()方法创建**一个新数组;**
* 这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成;

```js
var num = [4,19,23,31,18]
  
var numNum = num.map(function(item) {
  return item * item
})
  
console.log(num)
//[4, 19, 23, 31, 18]

console.log(numNum)
//[16, 361, 529, 961, 324]
```

## 8.3 reduce

arr.reduce

* 用于计算数组中所有元素的总和;

* 对数组中的每个元素按序执行一个由您提供的reducer 函数;
	* 如果没有提供，那么这个会使用数组**第一个数为返回值**
	* 简单数组是原始值，**复杂数组就是第一个对象**
	* **所以在对复杂数组进行计算的时候一定要对返回值进行初始话**
* 每一次运行 reducer 会将先前元素的计算结果作为参数传入，最后将其结果汇总为单个返回值;

**简单数组：**

```js
var bar = [2, 5, 29, 32, 19]
  
var num = bar.reduce(function(preVaduce, item) {
  return preVaduce + item
})

console.log(num)//87
```

**复杂数组**

```js
var bar = [
  {name: "axl", age: 19, height: 19.5},
  {name: "coder", age: 29, height: 20},
  {name: "wht", age: 20, height: 16.8}
]
  
var num = bar.reduce(function(preVaduce, item) {
  console.log(`preVaduce:${preVaduce}  item:${item.age}`)
  return preVaduce + item.age
},0)
/*
preVaduce:0  item:19
preVaduce:19  item:29
preVaduce:48  item:20
*/
  
console.log(num)//68
```
