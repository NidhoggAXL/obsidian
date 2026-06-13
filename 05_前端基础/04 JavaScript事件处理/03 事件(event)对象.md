# 一、认识event对象
当一个事件发生时，就会有和这个事件相关的很多信息:

* 比如事件的类型是什么，你点击的是哪一个元素，点击的位置是哪里等等相关的信息;
* 那么这些信息会被**封装到一个Event对象中**，这个对象由浏览器创建，称之为event对象
* 该对象给我们提供了想要的一些属性，以及可以通过该对象进行某些操作;

如何获取这个event对象呢?

* **event对象**会在**传入的事件处理(event handler)函数回调时**，被系统传入:
* 我们可以在回调函数中拿到这个event对象;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728549164000rihtb9.png)


# 二、event常见的属性和方法

常见的属性:

* **type**:事件的类型;
* **target**:当前事件发生的元素;
* **currentTarget**:当前处理事件的元素
* **eventPhase**:事件所处的阶段[[02 事件冒泡捕获#^d8d748|冒泡、捕获]]
* offsetX、offsetY:事件发生在元素内的位置;
* clientX、clientY:事件发生在客户端内的位置;
* pageX、pageY:事件发生在客户端相对于document的位置:
* screenX、screenY:事件发生相对于屏幕的位置

>[!tip] target 和 currentTarget 的区别：
>* target 是事件发生的源头
>* currentTarget 是当前通过事件冒泡处理的元素

```html
<div class="box">
  <button data-action="add">增加</button>
  <button data-action="remove">删除</button>
  <button data-action="edit">修改</button>
</div>

<script>
  var divEl = document.querySelector(".box")
  divEl.onclick = function(event) {
    console.log(event.target)
    console.log(event.currentTarget)
  }
</script>
```

点击删除按钮：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1734166703000dgo5i5.png)
	

> [!tip] **常见的方法**:
> * preventDefault:取消事件的默认行为;
> 	* 例如 a 元素的跳转 URL
> * stopPropagation:阻止事件的进一步传递(冒泡或者捕获都可以阻止)
