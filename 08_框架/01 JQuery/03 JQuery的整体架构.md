# 一、jQuery架构设计图
在开始学习jQuery语法之前，我们先来了解一下jQuery的架构设计图。

jQuery架构设计图如下:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737638178000hjts7y.png)

```js
;(function(global, factory) {
 factory(global)
})(window, function(window) {
 function XLjQuery(selector) {
  //new 操作会创建一个对象
  return new XLjQuery.fn.init(selector)
 }
  
 //原型方法
 XLjQuery.prototype = {
  constructor: XLjQuery,
  extend: function() {},
  text: function() {}
 }
 //XLjQuery类方法
 XLjQuery.noConflict = function() {}
 XLjQuery.map = function() {}
 XLjQuery.fn = XLjQuery.prototype
  
 //构造函数（创建jquery对象）
 XLjQuery.fn.init = function(selector) {//css selector
  if (!selector) return this
  var el = document.querySelector(selector)
  this[0] = el
  this.length = 1
  return this
 }

 XLjQuery.fn.init.prototype = XLjQuery.fn
 window.XLjQuery = window.$ = XLjQuery
})
```


# 二、jQuery的选择器（selecotors）
jQuery函数支持大部分的CSS选择器，语法:jQuery('字符串格式的选择器")

1. 通用选择器`(*)`
2. **基本选择器(id, class, 元素)**
3. 属性选择器`([attr],[atrr="value"])`
4. 后代选择器(div>span，div span)
5. 兄弟选择器(div+span,div~span)
6. 交集选择器(div.container)
7. **伪类选择器**(:nth-child()，:nth-of-type0)，:not0)，但不支持状态伪类 :hover, :focus..)
8. 内容选择器(:empty，:has(selector),empty指选中的元素没有子元素或文本; has指选中的元素是否存在某个子元素
9. 可见选择器(:visible，:hidden)
10. **jQuery扩展选择器:(:eq()-参数为索引,:odd(偶数选择器),:even(奇数选择器), :first, :last )**

```js
$('字符串')
```

# 三、VSCode代码片段

生线生成代码片段地址:https://snippet-generator.app/

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1737702433000t98brn.png)


# 四、jQuery过滤器（filtering）的API

jQuery过滤器API(即jQuery原型上的方法)

1. **eq(index)**:从匹配元素的集合中，取索引处的元素，eq全称(equal 等于)，返回jQuery对象.
2. **first()**:从匹配元素的集合中，取第一个元素，返回jQuery对象。
3. **last()**:从匹配元素的集合中，取最后一个元素，返回jQuery对象。
4. **not(selector)**:从匹配元素的集合中，删除匹配的元素，返回jQuery对象,过滤出匹配的元素，返回jQuery对象。
5. **filter(selector)**:从匹配元素的集合中，过滤没有匹配到的，返回jQuery对象。
6. **find(selector)**:从匹配元素集合中，找到匹配的后代元素，返回jQuery对象,
7. **sibings(selector)**:从匹配元素集合中，找到兄弟元素。
8. is(selectorlelement| .):根据选择器、元素等检査当前匹配到元素的集合。集合中至少有一个与给定参数匹配则返回true。
9. odd() :将匹配到元素的集合减少为集合中的奇数，从零开始编号，返回jQuery对象。
10. even():将匹配到元素的集合减少到集合中的偶数，从零开始编号，返回iQuery对象。
11. **大部分支持链式调用**
12. ……

```js
$('ul li').add()
$('ul li').even()
```

**链式调用：**

```js
$('ul ll').filter('.li-2, .li-3').eq(1)
```




