# 一、认识
Moment库，官网的描述:

* Moment 是一个 JavaScript 库，可以帮助我们**快速处理时间和日期**，已在数百万的项目中使用。
* Moment**对浏览器的兼容性比较好**，例如，在Internet Explorer 8+版本运行良好。
* 现在比较多人反对使用 Moment是因为**它的包大小**。Moment不适用于“**tree-shaking”算法**，因此往往会增加 Web 应用程序包的大小。如果需要国际化或时区支持，Moment可以变得相当大。
* **Moment团队**也希望我们在未来的新项目中**不要使用Moment** 。而推荐使用其它的替代品。例如:Day.js。

> [!tip] tree-shaking算法（摇晃树）
这种算法就是，当一个库里面有一些函数没有被使用到的时候，整个程序打包的时候，就可以把没有使用的不进行一个打包，这样就可以减少包的大小。

Day.js库，官网的描述:

* Dayjs 是 Moment的缩小版。Day,js 拥有与 Moment相同的 API，并将其文件大小减少了 97%。
* Moment完整压缩文件的大小为 67+Kb，**Dayjs 压缩文件只有 2Kb.**
* Dayjs所有的 AP| 操作都将**返回一个新的 Day,js 对象**，这种设计能避免 bug 产生，减少调试时间。
* Day.js 对**国际化支持良好**。国际化需手动加载，多国语言默认是不会被打包到Dayjs中的。

# 二、Day.js库安装

方式一:CND
*  https://unpkg.com/dayjs@1.8.21/dayjs.min.js

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741871931000newlsy.png)

方式二：下载源码引入

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741871957000q04sad.png)


# 三、Day.js简单的构架
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17418747880009jn0ll.png)


其中为什么要 `dayjs.prototype = Dayjs.prototype` 有这一代码：

* 这样就可以得到下面的这样代码啦

```js
  dayjs().format()

  var c = new dayjs()
  c.format()
```

可以使用 new 操作来创建一个 dayjs 对象，直接使用 Dayjs 函数原型上面的方法。多出了一个 new 的操作。

```js
//同时这样就可以进行链式调用啦
var c = dayjs().
```

# 四、获取设置时间
获取(Get)+ 设置(Set)

* .year()、.month、.date()--获取年、月、日
* .hour()、.minute()、.second()-获取时、分、秒
* .day()-获取星期几
* .format()-格式化日期

```js
<script>
 //1.获取是时间
 var date1 = dayjs()
 console.log( date1.year() , date1.month() + 1 , date1.date() )//2025 3 14
 console.log( date1.format() )//2025-03-14T15:49:10+08:00
  
 //2.设置时间
 var date2 = dayjs().year(2000).month(3).date(17)
 console.log( date2.year() , date2.month() + 1 , date2.date() )//2000 4 17
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741940224000k1n0fe.png)

# 五、时间操作

操作日期和时间(unit-单位)

* .add(numbers，unit)-添加时间
* .subtract(numbers,unit)-减去时间
* .startOf(unit)- 时间的开始

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741939639000yao28m.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741940211000ukvttq.png)

# 六、时间解析
解析时间

* dayjs(毫秒|秒)- 时间戳(毫秒 和 秒)
* dayjs(2022-06-15')- 1SO 8601格式的字符串
* dayjs(new Date())-接收日期对象

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17419413480004b8axd.png)

# 七、插件的使用

Day.js的插件应用

* .fromNow()-从现在开始的时间(需要依赖:relativeTime 插件)
* relativeTime插件:
	* https://cdn,jsdelivr.net/npm/dayjs@1.11.3/plugin/relativeTime.js

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741943819000afx6w3.png)

# 八、对UTC时间的处理

## 8.1 认识UTC

**UTC（协调世界时）是一个全球通用的、高精度的标准时间基准，可以将其理解为现代的“世界标准时间”。**

1. **时区关系**：
    
    - 北京时间 = UTC + 8小时
    - 东京时间 = UTC + 9小时
    - 伦敦时间 = UTC + 0小时（冬季）/ UTC + 1小时（夏季）
    - 纽约时间 = UTC - 5小时（东部标准时间）
2. **常见格式**：
    
    - ISO 8601格式：2023-12-25T10:30:00Z
    - RFC 2822格式：Sun, 25 Dec 2023 10:30:00 GMT
    - 数字格式：20231225103000Z
3. **在编程中的应用**：
    
    - 数据库存储通常使用UTC时间
    - API接口传递时间建议使用UTC
    - 前端展示时再转换为本地时间

## 8.2 装换UTC

UTC 增加了 `.utc` `.local` `.isUTC` APIs 使用 UTC 模式来解析和展示时间。

```javascript
var utc = require("dayjs/plugin/utc");
// import utc from 'dayjs/plugin/utc' // ES 2015

dayjs.extend(utc);

// default local time
dayjs().format(); //2019-03-06T17:11:55+08:00

// UTC mode
dayjs.utc().format(); // 2019-03-06T09:11:55Z

// convert local time to UTC time
dayjs().utc().format(); // 2019-03-06T09:11:55Z

// While in UTC mode, all display methods will display in UTC time instead of local time.
// 所有的 get 和 set 方法也都会使用 Date#getUTC* 和 Date#setUTC* 而不是 Date#get* and Date#set*
dayjs.utc().isUTC(); // true
dayjs.utc().local().format(); //2019-03-06T17:11:55+08:00
dayjs.utc("2018-01-01", "YYYY-MM-DD"); // with CustomParseFormat plugin
```

默认情况下，Day.js 会把时间解析成本地时间。

Day.js 默认使用用户本地时区来解析和展示时间。 如果想要使用 UTC 模式来解析和展示时间，可以使用 `dayjs.utc()` 而不是 `dayjs()`

### [dayjs.utc](https://day.js.org/docs/zh-CN/plugin/utc#dayjsutc-dayjsutcdatetype-string-number-date-dayjs-format-string)

`dayjs.utc(dateType?: string | number | Date | Dayjs, format? string)`

返回一个使用 UTC 模式的 `Dayjs` 对象。

### [Use UTC time ](https://day.js.org/docs/zh-CN/plugin/utc#use-utc-time-utc)

`.utc()`

返回一个复制的包含使用 UTC 模式标记的 `Dayjs` 对象。

### [Use local time](https://day.js.org/docs/zh-CN/plugin/utc#use-local-time-local) 

`.local()`

返回一个复制的包含使用本地时区标记的 `Dayjs` 对象。

### [Set UTC offset ](https://day.js.org/docs/zh-CN/plugin/utc#set-utc-offset-utcoffset)

`.utcOffset()`

返回一个复制的使用 UTC 模式的 Day.js 对象。

### [isUTC mode](https://day.js.org/docs/zh-CN/plugin/utc#isutc-mode-isutc) 

`.isUTC()`

返回一个 `boolean` 来展示当前 Day.js 对象是不是在 UTC 模式下。


## 8.3 装换封装

```ts
import dayjs from 'dayjs'
import utc from "dayjs/plugin/utc"
dayjs.extend(utc)

export function formatDayjs(utcString: string, format = "YYYY-MM-DD HH:mm:ss") {
  return dayjs.utc(utcString).utcOffset(8).format(format)
  //  使用 dayjs 库处理 UTC 时间格式转换 将 UTC 时间字符串转换为东八区（北京时间）的格式化时间字符串 参数 utcString: UTC 格式的时间字符串 参数 format: 目标格式，如 'YYYY-MM-DD HH:mm:ss' 返回: 转换后的格式化时间字符串
}

```



