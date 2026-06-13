# 一、认识事件委托
事件冒泡在某种情况下可以帮助我们实现强大的事件处理模式 – 事件委托模式（也是一种设计模式）

那么这个模式是怎么样的呢？ 

* 因为当子元素被点击时，父元素可以通过冒泡可以监听到子元素的点击； 
* 并且可以通过event.target获取到当前监听的元素； 

**案例：一个ul中存放多个li，点击某一个li会变成红色** 

* 方案一：监听每一个li的点击，通过遍历每次进行判断，并且做出相应；
* 方案二：在ul中监听点击，并且通过event.target拿到对应的li进行处理；
	* 因为这种方案并不需要遍历后给每一个li上添加事件监听，所以它更加高效；

```js
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>

  <script>
    // 1.拿到ul元素
    var ulEls = document.querySelector("ul")
    //2.设置变量来监听事件是否发生过
    var detection = null
    //3.event里面包含了事件的全部内容
    ulEls.onclick = function(event) {
      //4.判断是否前面发生过事件
      //发生过就移除clss
      if(detection && event.target !== ulEls) {
        //移除clss
        detection.classList.remove("active")
      }
      //判断点击的源是否在li上
      if(event.target !== ulEls) {
        //不在ul上，则为li添加class
        event.target.classList.add("active")
      }
      //记录添加clss的元素
      detection = event.target
    }
  </script>
</body>
```


# 二、事件委托标记

某些事件委托可能需要对具体的子组件进行区分，这个时候我们可以使用`data-*`对其进行标记：

比如多个按钮的点击，区分点击了哪一个按钮：

```js
<body>
  <div class="box">
    <button data-action="add">增加</button>
    <button data-action="remove">删除</button>
    <button data-action="edit">修改</button>
  </div>

  <script>
    var divEl = document.querySelector(".box")
    divEl.onclick = function(event) {
      var btnEl = event.target
      var action = btnEl.dataset.action
      switch (action) {
        case "add":
          console.log("增加")
          break
        case "remove":
          console.log("删除")
          break
        case "edit":
          console.log("修改")
          break
      }
    }
  </script>
</body>
```



