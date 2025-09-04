
# 一、Router的使用

react-router最主要的API是给我们提供的一些组件： 

BrowserRouter或HashRouter 

- Router中包含了对路径改变的监听，并且会将相应的路径传递给子组件； 
- **BrowserRouter** 使用history模式； 
- **HashRouter** 使用hash模式；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755679780000753wvx.png)

# 二、路由映射表配置

Routes：包裹所有的Route，在其中匹配一个路由 

- Router5.x使用的是Switch组件 

Route：Route用于路径的匹配；

- **path属性**：用于设置匹配到的路径； 
- **element属性**：设置匹配到路径后，渲染的组件；
	- Router5.x使用的是component属性 
- exact：精准匹配，只有精准匹配到完全一致的路径，才会渲染对应的组件； 
	- <mark class="hltr-orange">Router6.x不再支持该属性</mark>

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755680803000jl98x3.png)

# 三、路由配置和跳转

Link和NavLink： 

- 通常路径的跳转是使用Link组件，最终会被渲染成a元素； 
- [[06 Router的配置方式#1. 路由跳转|NavLink]]是在Link基础之上增加了一些样式属性（后续学习）； 
- to属性：Link中最重要的属性，用于设置跳转到的路径；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755680785000v48czy.png)

Link也有其他的一些属性设置：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755680953000ceopla.png)

# 四、NavLink的使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755681703000tb1ft3.png)

# 五、Navigate导航

Navigate用于路由的重定向，当这个组件出现时，就会执行跳转到对应的to路径中： 

我们这里使用这个的一个案例： 

- 用户跳转到Profile界面； 
- 但是在Profile界面有一个isLogin用于记录用户是否登录：
	- true：那么显示用户的名称； 
	- false：直接重定向到登录界面；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556885110001rshux.png)

我们也可以在匹配到`/`的时候，直接跳转到`/home`页面

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755688533000qd9qg6.png)

# 六、Not Found页面配置

如果用户随意输入一个地址，该地址无法匹配，那么在路由匹配的位置将什么内容都不显示。 

很多时候，我们希望在这种情况下，让用户看到一个Not Found的页面。 

这个过程非常简单： 

- 开发一个Not Found页面； 
- 配置对应的Route，**并且设置`path为*`即可；**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755688652000d3mzwr.png)





