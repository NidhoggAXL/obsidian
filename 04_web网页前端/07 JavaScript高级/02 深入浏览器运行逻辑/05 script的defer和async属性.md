# 一、defer属性
defer 属性告诉浏览器不**要等待脚本下载，而继续解析HTML，构建DOM Tree.**

* 脚本会由浏览器来进行下载，但是不会阻塞DOM Tree的构建过程;
* 如果脚本提前下载好了，它会等待DOM Tree构建完成，在**DOMContentLoaded（DOM内容加载完成）事件之前先执行defer中的代码**

![[script的defer属性作用效果图]]


所以DOMContentLoaded总是会等待defer中的代码先执行完成

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1730725933000wg4hxw.png)

**另外多个带defer的脚本是可以保持正确的顺序执行的**

```js
<body>
  <div class="box">box</div>
  
  <script defer>第一个脚本</script>
  <script defer>第二个脚本</script>
</body>
```

> 一定会等第一个脚本执行完，才会指向第二个脚本

**从元素中:某种角度来说，defer可以提高页面的性能，并且推荐放到head**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17307260740003nmbbu.png)


> [!tip] 注意:
> defer仅适用于外部脚本（使用 src 引用的），对于script默认内容（直接在script里面编写代码）会被忽略

# 二、async属性
async 特性与 defer 有些类似，它也能够让脚本不阻塞页面。

async是让一个脚本完全独立的:

* 浏览器**不会因 async 脚本而阻塞**(与 defer 类似)
* async脚本**不能保证顺序**，它是独立下载、独立运行，不会等待其他脚本
* async**不能保证在DOMContentLoaded之前或者之后执行**


# 三、开发中两属性的选择
defer通常用于需要在文档解析后操作DOM的JavaScript代码，并且对多个script文件有顺序要求的;

async通常用于独立的脚本，对其他脚本，甚至DOM没有依赖的;

