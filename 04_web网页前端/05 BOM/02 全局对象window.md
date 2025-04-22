# 一、认识window对象

window对象在浏览器中可以从两个视角来看待:

* 视角一:**全局对象**。
	* 我们知道ECMAScript其实是有一个全局对象的，这个全局对象在Node中是global
	* 在浏览器中就是window对象:
* 视角二:**浏览器窗口对象**。
	* 作为浏览器窗口时，提供了对**浏览器操作的相关的API;**


当然，这两个视角存在大量重叠的地方，所以不需要刻意去区分它们:

* 事实上**对于浏览器和Node中全局对象名称不一样的情况**，目前已经指定了对应的标准，称之为**alobalThis**，并且大多数现代浏览器都支持它;
* 放在**window对象**上的所有属性都可以被访问;
* 使用**var定义的变量会被添加到window对象中**:
* window默认给我们提供了全局的函数和类:**setTimeout、Math、Date、Object**等;

# 二、window对象的作用
事实上window对象上肩负的重担是非常大的:

* 第一:包含大量的属性，localStorage、console、location、history、screenX、scrollX等等(大概60+个属性);
* 第二包含大量的方法，alert、close、scrollTo、open等等(大概40+个方法);
* 第三:包含大量的事件，focus、blur、load、hashchange等等(大概30+个事件);
* 第四:包含从EventTarget继承过来的方法，addEventListener、removeEventListener、dispatchEvent方法


那么这些大量的属性、方法、事件在哪里查看呢?

* MDN文档:https://developer.mozilla.org/zh-CN/docs/Web/APl/Window

# 三、window常见的属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1729171152000xv4jda.png)

# 四、window常见的方法
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1729171611000y6bn8m.png)


# 五、window常见的事件
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1729171808000e85cy4.png)

哈希值是上面呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1729171858000uh24r9.png)

后面的 index 就是哈希值，这和前端路由有关系。