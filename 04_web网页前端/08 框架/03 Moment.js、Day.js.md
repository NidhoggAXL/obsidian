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





