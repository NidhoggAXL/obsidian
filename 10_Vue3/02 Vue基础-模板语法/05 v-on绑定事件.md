
# 一、v-on绑定事件

前面我们绑定了元素的内容和属性，在前端开发中另外一个非常重要的特性就是交互

在前端开发中，需要经常和用户进行各种各样的交耳:

- 就必须监听用户发生的事件，比如点击、拖拽、键盘事件等等
- 在Vue中如何监听事件呢?使用 **v-on** 指令

# 二、v-on的用法
v-on的使用:

* 缩写: `@`
* 预期: `Function | Inline Statement | Object`
* 参数: `event`
* 修饰符
	* `.stop` - 调用 [[03 事件(event)对象|event.stopPropagation()]]。
	* `.prevent` - 调用 [[03 事件(event)对象|event.preventDefault()]]。
	* `.capture` - 添加事件侦听器时使用 capture 模式。
	* `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
	* `.{keyAlias}` - 仅当事件是从特定键触发时才触发回调。
	* `.once` - 只触发一次回调。
	* `.left` - 只当点击鼠标左键时触发。
	* `.right` - 只当点击鼠标右键时触发。
	* `.middle` - 只当点击鼠标中键时触发。
	* `.passive` - `{passive:true}` 模式添加侦听器。
* 用法:绑定事件监听
# 三、v-on的基本使用


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745586494000qwfcty.png)

# 四、v-on参数传递

当通过methods中定义方法，以供 `@click` 调用时，需要注意参数问题:

- 情况一:如果该方法不需要额外参数，那么方法后的 `()` 可以不添加。
	- **但是注意**:如果方法本身中有一个参数，那么会**默认将原生事件 event 参数传递进去**
- 情况二:如果需要同时传入某个参数，同时需要event时，可以通过 `$event` 传入事件



![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745646997000shk3ba.png)


# 五、v-on的修饰符


![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745647080000t82mu1.png)

**案例**：在 div 标签里面存在一个 button 按钮，当按钮发生点击的时候阻止发生其[[03 事件(event)对象|冒泡]]。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745647771000nfsh7o.png)










