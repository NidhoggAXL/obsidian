# 一、React事件绑定

如果原生DOM原生有一个监听事件，我们可以如何操作呢？ 

- 方式一：获取DOM原生，添加监听事件； 
- 方式二：在HTML原生中，直接绑定onclick；

在React中是如何操作呢？我们来实现一下React中的事件监听，这里主要有两点不同 

- React 事件的命名采用**小驼峰式（camelCase）**，而不是纯小写； 
- 我们需要**通过{}传入一个事件处理函数**，这个函数会在事件发生时被执行；

```html
<button onClick={Function}>按钮点击</button>
```

#  二、this的绑定问题

在事件执行后，我们可能需要获取当前类的对象中相关的属性，这个时候需要用到this 

- 如果我们这里直接打印this，也会发现它是一个undefined 

**为什么是undefined呢？** [[03 React组件化的封装#三、事件绑定|事件绑定]]

- 原因是btnClick函数并不是我们主动调用的，而且当button发生改变时，**React内部调用了btnClick函数**； 
- 而它内部调用时，并不知道要如何绑定正确的this；

**如何解决this的问题呢？** 

- **方案一**：bind给btnClick显示绑定this 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754985165000hwwuz5.png)

- **方案二**：使用 ES6 class fields 语法 

> [!tip] 什么是 fields 语法
> ![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175498559400068jwga.png)

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754985665000gtwlxx.png)


- **方案三**：事件监听时传入箭头函数

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754985873000e3f9zq.png)

> React 做的本质就是把 this.btnClick() 的执行结果给返回了，并没有执行 btnClik 本身。
# 三、事件参数传递
在执行事件函数时，有可能我们需要获取一些参数信息：比如event对象、其他参数 

* **情况一**：获取event对象 
	* 很多时候我们需要拿到event对象来做一些事情（比如阻止默认行为） 
	* 那么默认情况下，event对象有被直接传入，函数就可以获取到event对象； 
- **情况二**：获取更多参数 
	- 有更多参数时，我们最好的方式就是传入一个箭头函数，主动执行的事件函数，并且传入相关的其他参数；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754987427000y7hak2.png)

# 四、参数传递案例

点击不同的 movies 列表，更具点击改变点击的颜色：

<div style="
  height: 500px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754988942000tjzejj.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>




 