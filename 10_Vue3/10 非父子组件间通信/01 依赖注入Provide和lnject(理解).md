# 一、proviede和inject

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746792832000o7j1j7.png)

# 二、Provide和Inject基本使用

我们开发一个这样的结构：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746792850000u7yt2o.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746792867000oodc26.png)

# 三、Provide和Inject函数的写法

如果Provide中提供的一些数据是<mark class="hltr-orange">来自data</mark>，那么我们可能会想要<mark class="hltr-orange">通过this来获取</mark>：

这个时候会报错： 这里使用thsi的话，**这个this是指向全局的，并不是data里面的数据**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746793029000s2yn84.png)

就会报如下的错误：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17467930390006c9b89.png)

<mark class="hltr-orange">解决这个错误就是使用函数写法：</mark>这样this就是指向provide的，provide在vue的内部会把这个函数的this指向data，这样就可以正确的拿到data里面的数据了。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746793073000jn6jcc.png)

# 四、处理响应式数据

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746793278000lmm3nc.png)



