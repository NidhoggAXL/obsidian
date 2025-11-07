# 一、JavaScript编写方式
方式一：HTML代码行内（不推荐）

```html
<a href="#" onclick="alert('百度一下')">百度一下</a>
```

方式二：script标签中

```html
<a class="google" href="#">Google一下</a>
<script>
	var googleAE1 = document.querySelector(".google")
	googleAE1.onclick = function(){
		alert("Google")
	}
</script>
```

方式三：外部的script文件

* 通过script元素的src属性来引入js代码

```html
<a class="bing" href="#">bing一下</a>
<script src="./js/bing.js"></script>
```

# 二、`<noscript>`元素
如果运行的浏览器不支持JavaScript,那么我们如何给用户更好的提示呢?

* 针对早期浏览器不支持 JavaScript 的问题，需要一个页面优雅降级的处理方案;
* 最终，`<noscript>`元素出现，被用于给不支持JavaScript 的浏览器提供替代内容;

下面的情况下,浏览器将显示包含在`<noscript>`中的内容:

* 浏览器不支持脚本;
* 浏览器对脚本的支持被关闭。

```html
<body>
	<noscript>
		<h1>你的浏览器不支持或者关闭了js</h1>
	</noscript>
</body>
```


# 三、JavaScript编写注意事项
注意-: script元素**不能写成单标签**

* 在外联式引用js文件时，script标签中不可以写JavaScript代码，并且script标签不能写成单标签;
* 即不能写成`<script src=“index.js”/>;`

注意二:省略type属性

* 在以前的代码中，`<script>`标签中会使用`type=“text/javascript”`;
* 现在可不写这个代码了，因为**JavaScript 是所有现代浏览器以及 HTML5 中的默认脚本语言;**

注意三: 加载顺序

* 作为HTML文档内容的一部分，JavaScript默认遵循HTML文档的加载顺序，即自上而下的加载顺序
* 推荐将JavaScript代码和**编写位置放在body子元素的最后一行**;
	* 虽然可以放到body与html标签里面，也可以放到html外边

注意四:JavaScript代码严格区分大小写

* **HTML元素和CSS属性不区分大小写，但是在JavaScript中严格区分大小写;**


后续补充:script元素还有defer、async属性


# 四、JavaScript交互方式

JavaScript有如下和用户交互的手段:

最常见的是通过console.log,目前大家掌握这个即可;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17272694300009312wf.png)

|  alert   | 警告  |
| :------: | :-: |
| console  | 控制台 |
|   log    | 日志  |
| document | 文档  |
|  write   |  写  |
|  prompt  | 提示  |

# 五、Chrome调试工具
在前面我们利用Chrome的调试工具来调试了HTML、CSS，它也可以帮助我们来调试JavaScript。

当我们在JavaScript中通过console函数显示一些内容时，也可以使用Chrome浏览器来查看:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1727269756000jzlwev.png)

另外补充:

* 如果在代码中**出现了错误**，那么可以在**console中显示错误**
* console中有个 > 标志，它表示控制台的命令行
	* 在命令行中我们可以直接编写JavaScript代码，**按下enter会执行代码:**
	* 如果希望编写多行代码，可以按下**shift+enter来进行换行编写;**
* 在后续我们还会学习如何**通过debug方式来调试、查看代码的执行流程**

# 六、JavaScript语句和分号
语句是向浏览器发出的指令，通常表达一个操作或者行为(Action)

* 语句英文是Statements;
* 比如我们前面编写的每一行代码都是一个语句，用于告知浏览器一条执行的命令;

通常每条语句的后面我们会添加一个分号，表示语句的结束:

* 分号的英文是semicolon
* 当存在换行符(line break)时，**在大多数情况下可以省略分号**
* JavaScript 将换行符**理解成“隐式”的分号**;
* 这也被称之为**自动插入分号(an automaticsemicolon)**

# 七、JavaScript注释

JavaScript的注释主要分为三种:

**单行注释**

```
//单行注释
不过可以全部选择后面快捷键 ctrl+/ 就全部注释了
```


**多行注释**

```
/* 多行注释 */
```

**文档注释**(VSCode中需要在单独的JavaScript文件中编写才有效)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17272727220001ka82g.png)

```
/**(简写) 在按huiche vscoder 的自带插件就会进行文档的注释
每一个注释写完按 tab 键就会跳转到下一个注释点
```

> [!tip] 注意:
> JavaScript也不支持注释的嵌套

# 八、VSCode插件和配置
ES7+ React/Redux/React-Native snippets

* 这个插件是在react开发中会使用到的，但是我经常用到它里面的打印语句;（clg -> enter)








