
# 一、v-on绑定事件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745586515000qabh4b.png)
# 二、v-on的用法
v-on的使用:

* 缩写:@
* 预期:Function |Inline Statement|Object
* 参数:event
* 修饰符
	* .stop-调用 [[03 事件(event)对象|event.stopPropagation()]]。
	* .prevent-调用 [[03 事件(event)对象|event.preventDefault()]]。
	* .capture-添加事件侦听器时使用 capture 模式。
	* .self-只当事件是从侦听器绑定的元素本身触发时才触发回调。
	* .{keyAlias}- 仅当事件是从特定键触发时才触发回调。
	* .once-只触发一次回调。
	* .left-只当点击鼠标左键时触发。
	* .right-只当点击鼠标右键时触发。
	* .middle-只当点击鼠标中键时触发。
	* .passive-{passive:true}模式添加侦听器。
* 用法:绑定事件监听
# 三、v-on的基本使用


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745586494000qwfcty.png)

# 四、v-on参数传递

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745646407000s5v8zn.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745646997000shk3ba.png)


# 五、v-on的修饰符


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745647080000t82mu1.png)

案例：在 div 标签里面存在一个 button 按钮，当按钮发生点击的时候阻止发生其冒泡。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745647771000nfsh7o.png)










