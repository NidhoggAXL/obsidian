# 一、Math对象
在除了Number类可以对数字进行处理之外，JavaScript还提供了一个Math对象

* Math是一个内置对象(不是一个构造函数)，"**它拥有一些数学常数属性和数学函数方法**":

Math常见的属性:

* Math.Pl:圆周率，约等于 3.14159;

```js
console.log(Math.PI)
//3.141592653589793
```

Math常见的方法:

* **Math.floor**:向下舍入取整(floor-地板)
* **Math.ceil**:向上舍入取整(ceil-天花板)
* **Math.round**:四舍五入取整(round-圆形的)
* **Math.random**:生成0~1的随机数（包含0，不包含1）
* **Math.pow(x,y)**:返回x的y次幂

```js
var a = 2.54

console.log(Math.floor(a))//2
console.log(Math.ceil(a))//3
console.log(Math.round(a))//3
```

Math中还有很多其他数学相关的方法，可以查看MDN文档:
https://developer.mozillarog/docs/Web/avaScript/Reference/Global_obiects/Math