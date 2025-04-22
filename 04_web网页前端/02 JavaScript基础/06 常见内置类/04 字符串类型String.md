# 一、基本使用
String常见的属性:

* length:获取字符串的长度;


操作一:访问字符串的字符

* 使用方法一:通过字符串的索引 `str[0]`
* 使用方法二:通过str.charAt(pos)方法
* 它们的区别是索引的方式没有找到会返回undefined，而charAt没有找到会返回空字符串

```js
var message = "hello world"
console.log(message[0])//h
console.log(message.charAt(0))//h

console.log(message[20])//空
console.log(message.charAt(20))//undefined
```

字符串的遍历：

方式一：普通for循环

```js
var message = "hello world"
for (var i = 0; i < message.length; i++) {
  console.log(message[i])
}
```

方式二：for...of 遍历

```js
var message = "hello world"
for (var char of message) {
  console.log(char)
}
```

# 二、修改字符串
字符串的不可变性:

* 字符串在定义后是不可以修改的，所以下面的操作是没有任何意义的，

```js
var message = "hello world"
message[0] = "a"
console.log(message)//hello world
```

所以，在我们改变很多字符串的操作中，**都是生成了一个新的字符串;**

* 比如改变字符串大小的两个方法
* **toLowerCase0()**:将所有的字符转成小写;
* **toUpperCase()**:将所有的字符转成大写;

```js
var message = "hello world"

var messageA = message.toUpperCase()
console.log(message)//hello world
console.log(messageA)//HELLO WORLD
```


# 三、查找字符串

在开发中我们经常会在一个字符串中查找或者获取另外一个字符串，String提供了如下方法:

方法一:查找字符串位置`str.indexOf(searchValue[ ,fromIndex])`

* 从fromIndex开始，查找searchValue的索引;
* 找到返回找到的索引
* 如果没有找到，那么返回-1:
* 有一个相似的方法，叫lastIndexOf，从最后开始查找(用的较少)

```js
var message = "hello world"
var bar = "world"

//查找是否存在字符串
console.log(message.indexOf(bar))//6
console.log(message.indexOf(bar[7]))//-1
```


方法二:是否包含字符串`str.includes(searchString[,position])`

* 从position位置开始查找searchString，根据情况返回 true 或 false
* 这是ES6新增的方法;

```js
var message = "hello world"
var bar = "world"

console.log(message.includes(bar))//true
```

方法三:以xxx开头`str.startsWith(searchString[，position])`

* 从position位置开始，判断字符串是否以searchString开头;
* 这是ES6新增的方法，下面的方法也一样:

方法四:以xxx结尾`str.endswith(searchstringl[,length])`

* 在length长度内，判断字符串是否以searchString结尾;

```js
var message = "hello world"
var bar = "world"

// 是否xxx开头或者结尾
console.log(message.startsWith(bar))//fales
console.log(message.endsWith(bar))//true
```

方法五:替换字符串str.replace(regexp substr,newSubStr function)

* 查找到对应的字符串，并且使用新的字符串进行替代;
* 这里也可以传入-个正则表达式来查找，也可以传入一个函数来替换;

```js
var message = "hello world"
var bar = "world"

var newMessage = message.replace("world", "coder")
console.log(newMessage)//hello coder
```

方法六：获取子字符串

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727613788000ejl7a6.png)


```js
var bar = "hello world"

console.log(bar.slice(3,-1))//lo worl
```

方法六:拼接字符串 `str.concat(str2，[,   ...strN])`

```js
var bar1 = "ab"
var bar2 = "cd"
var bar3 = "ef"

console.log(bar1.concat(bar2,bar3))//abcdef
```

方法七:删除首尾空格str.trim()


```js
var bar = "   axl    "

console.log(bar.trim())//axl
```

方法九:字符串分割 `str.split([separatorl[  ,limit]])`

* separator:以什么字符串进行分割，也可以是一个正则表达式
* limit:限制返回片段的数量;

```js
var bar = "my name is coder"

console.log(bar.split(" ",3))//['my', 'name', 'is']
```

MDN:https://developer,mozilla.org/zh-CN/docs/Web/javaScript/Reference/Global_Objects/String


