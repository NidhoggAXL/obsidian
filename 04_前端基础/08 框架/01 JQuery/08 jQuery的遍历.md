**.each( function): 遍历一个jQuery 对象，为每个匹配的元素执行一个回调函数。**
* function 参数:
	* Function(Integer index,Element element ),函数中返回false会终止循环。

```js
$('ul li').each(function(index, element) {
 console.log(index, element)
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738562875000iiyr22.png)

**jQuery.each(array | object，function):一个通用的选代器函数，可以用来无缝地选代对象和数组**

* array参数:支持数组(array)或者类数组(array-like),底层使用for循环
* object参数: 支持普通的对象 object 和 JSON对象等，底层用for in循环。
* function 参数:
	* Function( Integer index, Element element ),函数中返回false会终止循环。

源码如下：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1738563394000tfhq0c.png)

```js
jQuery.each($('ul li'), function(index, element) {
 console.log(index, element)
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17385630880005ffkxd.png)

**.each()和jQuery.each()函数的区别:**

* .each()是jQuery对象上的方法，**用于遍历jQuery对象,**
* jQuery.each()是jQuery函数上的方法，**可以遍历对象、数组、类数组等，它是一个通用的工具函数。**

```js
jQuery.each(["mba", "abc", "cba", "bbc"], function(index, element) {
 console.log(index, element)
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17385632200003y53ds.png)
