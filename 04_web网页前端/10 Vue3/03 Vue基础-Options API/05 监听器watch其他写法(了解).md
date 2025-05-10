# 一、监听器其他方式一


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745678181000h1l0dw.png)

# 二、监听器其他方式二

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456785430007fteis.png)

# 三、监听其他方式三

另外一个是Vue3文档中没有提到的，但是Vue2文档中有提到的是侦听对象的属性：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456785720006z43sr.png)

**还有另外一种方式就是使用 `$watch` 的API：**

我们可以在<mark class="hltr-orange">created的生命周期</mark>（[[01 组件的生命周期(重点)#二、生命周期的流程|生命周期]]）中，使用 this.$watchs 来侦听； 

* 第一个参数是要侦听的源； 
* 第二个参数是侦听的回调函数callback； 
* 第三个参数是额外的其他选项，比如deep、immediate；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456786170008lpim3.png)








