# 一、JSX的本质

实际上，jsx 仅仅只是 React.createElement(component, props, ...children) 函数的语法糖。 

- 所有的jsx最终都会被**转换成React.createElement的函数调用**。 

**createElement需要传递三个参数：**

- **参数一**：type 
	- 当前ReactElement的类型； 
	- 如果是标签元素，那么就使用字符串表示 “div”； 
	- 如果是组件元素，那么就直接使用组件的名称；
- **参数二**：config 
	- 所有jsx中的属性都在config中以对象的属性和值的形式存储； 
	- 比如传入className作为元素的class； 
- **参数三**：children 
	- 存放在标签中的内容，以children数组的方式进行存储； 
	- 当然，如果是多个元素呢？React内部有对它们进行处理，处理的源码在下方

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755000247000j1nmai.png)


# 二、Babel官网查看

我们知道默认jsx是通过babel帮助进行语法转换的，所以之前编写的jsx代码都需要依赖babel。 

可以在babel的官网中快速查看转换的过程: https://babeljs.io/repl/#?presets=react

```jsx
(
    <div>
        <h1 className="title">{message}</h1>
        <div>divElement</div>
        <ul>
            <li className="item">我是列表元素1</li>
            <li className="item">我是列表元素2</li>
            <li className="item">我是列表元素3</li>
            <li className="item">aoaoaooa</li>
        </ul>
    </div>
)
```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17550014000008awnbr.png)


# 三、直接编写jsx代码

自己来编写React.createElement代码： 

- 没有通过jsx来编写了，界面依然是可以正常的渲染。 
- 另外，在这样的情况下，你还需要babel相关的内容吗？不需要了 
	- 所以，type="text/babel"可以被我们删除掉了； 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755001766000dm8ggg.png)

# 四、虚拟DOM的创建过程

通过 React.createElement 最终创建出来一个 ReactElement对象：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755002825000vqjsex.png)

这个ReactElement对象是什么作用呢？React为什么要创建它呢？ 

- 原因是React利用ReactElement对象组成了一个**JavaScript的对象树**； 
- JavaScript的对象树**就是虚拟DOM（Virtual DOM）**；

如何查看ReactElement的树结构呢？ 

- 我们可以将之前的jsx返回结果进行打印； 
- 注意下面代码中jsx的打印；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755002867000il1wlp.png)

> [!ps] 
> 
> **而ReactElement最终形成的树结构就是Virtual DOM；**

# 五、jsx–虚拟DOM–真实DOM

![[jsx-ReactElement-真实DOM|100%]]


# 六、声明式编程

虚拟DOM帮助从命令式编程转到了声明式编程的模式 

React官方的说法：Virtual DOM 是一种编程理念。 

- 在这个理念中，UI以一种理想化或者说虚拟化的方式保存在内存中，并且它是一个相对简单的JavaScript对象 
- 可以通过ReactDOM.render让 **虚拟DOM** 和 **真实DOM同步起来**，这个过程中叫做**协调（Reconciliation）**； 

这种编程的方式赋予了React声明式的API： 

- 你只需要告诉React希望让UI是什么状态； 
- React来确保DOM和这些状态是匹配的；
- 你不需要直接进行DOM操作，就可以从手动更改DOM、属性操作、事件处理中解放出来； 

> [!abstract]
>  虚拟DOM自我总结
>  
> - 虚拟DOM可以进行多端的使用，一次编写多端使用（因为都是JS对象）
> - 虚拟DOM赋予了声明式的编程
> - 虚拟DOM可以使用 differ 算法优化，让没有改变的不需要再次进行重置，提高效率


