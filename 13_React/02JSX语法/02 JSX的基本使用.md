# 一、注释

**jsx中的注释** :

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175496322300095od7g.png)

# 二、嵌入类型

**JSX嵌入变量作为子元素**：

- 情况一：当变量是Number、String、Array类型时，可以直接显示 
- 情况二：当变量是**null、undefined、Boolean**类型时，**内容为空**； 
	- 如果希望可以显示null、undefined、Boolean，那么需要转成字符串； 
	- 转换的方式有很多，比如toString方法、和空字符串拼接，String(变量)等方式； 
- 情况三：<mark class="hltr-orange">Object对象类型不能作为子元素</mark>（not valid as a React child） 
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754963546000uzwbc1.png)

# 三、嵌入表达式

**JSX嵌入表达式**：

- 运算表达式 
- 三元运算符 
- 执行一个函数

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754964739000gueq3f.png)

# 四、绑定属性

jsx绑定属性 

- 比如元素都会有title属性 
- 比如img元素会有src属性 
- 比如a元素会有href属性 
- 比如元素可能需要绑定class 
- 比如**原生使用内联样式style**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17549656340006xy53h.png)

## 4.1 绑定class

基础的绑定:

* 以前是不可以使用 calss 绑定的，因为这里是 JSX 代码，而 class 是一个关键字，不可以使用，要绑定 calss 必须使用 className 。
* 现在 babel 可以自动解析了，但是还是**建议使用 className**来绑定class。

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754969083000rp1eye.png)

动态绑定：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17549789010008duopr.png)

使用第三库：classnames

* https://github.com/JedWatson/classnames

## 4.2 内联样式style

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175497924100096ilrm.png)

> [!info] 不可以使用 font-size ，只可以使用小驼峰编写fontSize

> [!warning] Object不可以作为子元素，但是属性编写可以使用 Object

```jsx
//不可以使用，是错误的
<div>{Object}</div>

//可以在属性上面使用
<div style={Object}>哈哈哈</div>
```

