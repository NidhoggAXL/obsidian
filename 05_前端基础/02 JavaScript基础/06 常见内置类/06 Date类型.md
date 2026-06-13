# 一、时间的表示方法
**目前GMT依然在使用，主要表示的是某个时区中的时间，而UTC是标准的时间。**

# 二、时区对比图

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727787237000rsoqgc.png)

看上面的图也就可以想到中国的：东八区的这个说法。
# 三、创建Date对象

在JavaScript中我们使用Date来表示和处理时间，

* Date的构造函数有如下用法:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17279484830009p8m3n.png)

# 四、时间的两种标准表示方式
日期的表示方式有两种:RFC2822 标准 或者IS0 8601 标准。

**默认打印**的时间格式是RFC 2822标准的:

```js
new Date()
Fri May 13 2022 17:14:52 GMT+0800
```

我们也可以将其转化成ISO 8601标准的:

* YYYY:年份，0000~999
* MM:月份，01~12
* DD:日，01~31
* T:分隔日期和时间，没有特殊含义，可以省略
* HH:小时，00~24
* mm:分钟，00~59
* ss:秒，00~59
* .sss:毫秒
* Z:时区

```js
new Date().toIsostring()
'2022-05-13T09:15:51.507Z'
```

# 五、Date获取信息的方法

我们可以从Date对象中获取各种详细的信息:

* getFullyear():获取年份(4 位数);
* getMonth():获取月份，从0到11;
* getDate0:获取当月的具体日期，从1到31(方法名字有点迷)
* getHours():获取小时;
* getMinutes():获取分钟;
* getseconds():获取秒钟:
* getMilliseconds():获取亳秒;

获取某周中的星期几:

* getDay0):获取一周中的第几天，从0(星期日)到6(星期六);


# 六、Date设置信息的方法

Date也有对应的设置方法:

* `setFullYear(year, [month], [date])`
* `setMonth(month, [date])`
* `setDate(date)`
* `setHours(hour, [min], [sec], [ms])`
* `setMinutes(min, [sec], [ms])`
* `setSeconds(sec, [ms])`
* `setMilliseconds(ms)`
* `setTime(milliseconds)`

了解:我们可以设置超范围的数值，它会自动校准。

* 比如一个月有31天，如果设置超过了就会进行自动校验，把多出来的天数加到下个月。


# 七、Date获取Unix时间戳

Unix 时间戳:它是一个整数值，表示自1970年1月1日00:00:00 UTC以来的毫秒数。

在JavaScript中，我们有多种方法可以获取这个时间戳:

* 方式-:new Date().getTime()
* 方式二:new Date().valueOf()
* 方式三:+new Date()
* 方式四:Date.now()

# 八、Date.parse方法

Date.parse(str)方法可以从一个字符串中读取日期，并且输出对应的Unix时间戳

Date.parse(str):

* 作用**等同于 new Date(dateString).getTime()操作**,
* 需要**符合 RFC2822 或 IS0 8601 日期格式**的字符串
	* 比如YYYY-MM-DDTHH:mm:ss.sssZ
* 其他格式也许也支持，但**结果不能保证一定正常**
* 如果输入的格式不能被解析，那么会返回NaN;





