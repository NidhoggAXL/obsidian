# 一、什么是WXS?
WXS（WeiXin Script）是小程序的一套脚本语言，结合 WXML，可以构建出页面的结构。 

- 官方：WXS 与 JavaScript 是不同的语言，有自己的语法，并不和 JavaScript 一致。（不过基本一致） 

为什么要设计WXS语言呢？ 

- 在WXML中是**不能直接调用Page/Component中定义的函数**的. 
- 但是某些情况, 我们可以希望使用函数来处理WXML中的数据(类似于Vue中的过滤器)，这个时候就使用WXS了

WXS使用的限制和特点： 

- WXS **不依赖**于运行时的**基础库版本**，可以在所有版本的小程序中运行；
- WXS 的运行环境和其他 JavaScript 代码是隔离的，WXS 中**不能**调用其他 **JavaScript 文件中定义的函数**，也不能调用小程序 **提供的API**； 
	- <mark class="hltr-orange">但是可以调用 JavaScript 中 ES5 的 API</mark>
- 由于运行环境的差异，在 iOS 设备上小程序内的 WXS 会比 JavaScript 代码快 2 ~ 20 倍。在 android 设备 上二者运行效率 无差异；

>[!note] 为什么 WXS 是和 JavaScript 代码是隔离的。
>小程序是双线程的架构，一个线程是进行页面渲染的，一个页面是运行 js 代码的，而 **WXS 的运行环境是在页面渲染的线程中，就不会接触 js 代码。**
>- 在 WXS 的运行环境中不要编写大量逻辑代码，会影响页面的渲染
>- WXS 只能编写纯碎的 JS 代码

# 二、WXS语法基本使用

WXS有两种写法： 
- 写在标签中 
- 写在以.wxs结尾的文件中

`<wxs>` 标签的属性：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753623826000tjjfym.png)

每一个 .wxs 文件和`<wxs>`标签都是一个单独的模块。 

- 每个模块都有自己独立的作用域。即在一个模块里面定义的变量与函数，**默认为私有**的，对其他模块不可见；
- 一个模块要想对外暴露其内部的私有变量与函数，只能通过 [[02 CommonJS和Node#四、module.exports导出|module.wxports]] 实现；


# 三、WXS语法案例练习

## 3.1 练习一

使用两种方式来计算一个数组的和：

```js
<!-- 方式一:使用wxs脚本段 -->
<wxs module="total">
  function calcTotal(arr) {
    //使用 JS 的 reduce API
    return arr.reduce(function(preValue, value) {
      return preValue + value
    }, 0)
  }

  // 暴露私有变量和函数
  module.exports = {
    calcTotal: calcTotal
  }
</wxs>

<view>总和为：{{total.calcTotal(arr)}}</view>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17536248510001q4l3j.png)
## 3.2 练习二

案例练习题目： 

- 题目一：传入一个数字，格式化后进行展示（例如36456，展示结果3.6万）； 
- 题目二：传入一个时间，格式化后进行展示（例如100秒，展示结果为01:40）；

```js
//数量的单位计算
function formatCount(count) {
  count = Number(count)
  //toFixed保留小数位数
  if (count > 100000000) {
    return (count / 100000000).toFixed(1) + "亿"
  } else if ( count > 10000) {
    return (count / 1000).toFixed(1) + "万"
  } else { return count }
}

//保证 1 -> 01 的格式
function padLeft(time) {
  //wxs不支持String(time)，使用+来让数字变成字符串
  time = (time + "")
  //算法，slice是一个字符串截取函数
  return ("00" + time).slice(time.length)
}

//时间的持续时间
function formatDuration(duration) {
  var minute = Math.floor(duration / 60)
  var seconde = Math.floor(duration) % 60
  return padLeft(minute) + ":" + padLeft(seconde)
}

module.exports = {
  formatCount: formatCount,
  formatDuration: formatDuration
  //外部不使用padLeft，就不需要导出。
}
```

