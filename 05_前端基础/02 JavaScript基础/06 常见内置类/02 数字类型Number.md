Number属性补充:

* Number.MAX_SAFE_INTEGER:JavaScript 中最大的安全整数(2^53-1);
* Number.MIN_SAFE_INTEGER:JavaScript 中最小的安全整数-(2^53-1)

**Number实例方法补充:**

* 方法-:toString(base)，将数字转成字符串，并且按照base进制进行转
	* base 的范围可以从 2到 36，默认情况下是 10;
	* 注意:如果是直接对一个数字操作，需要使用[[06 展开运算符|...张开运算符]];

```js
var a = 100
var b = a.toString()

console.log(b)//100
console.log(typeof b)//string
```

* 方法二:toFixed(diqits)，格式化一个数字，保留digits位的小数;
	* 会**进行五舍六入**
	* digits的范围是0到20(包含)之间:

```js
var a = 100.12
var b = a.toFixed(3)

console.log(b)//100.120
console.log(typeof b) //string
```

Number类方法补充:

* 方法一:`Number.parselnt(string[, radix])`，将字符串解析成整数，也有对应的全局方法parselnt;
* 方法二:`Number. parseFloat(string)`，将字符串解析成浮点数，也有对应的全局方法parseFloat;


更多Number的知识，可以查看MDN文档:https://developer.mozilla.org/zh-CN/docs/Web/avaScript/Reference/Global_Objects/Number
