
如果我们编写一个js文件，里面存放JavaScript代码，如何来执行它呢?

**目前我们知道有两种方式可以执行**:

* 将代码交给浏览器执行
* 将代码载入到node环境中执行,

如果我们希望把代码交给浏览器执行:

* 需要通过让浏览器加载、解析html代码，所以我们需要创建一个html文件;
* 在html中通过script标签，引入js文件;
* 当浏览器遇到script标签时，就会根据src加载、执行JavaScript代码;

如果我们希望把js文件交给node执行:

* 首先电脑上需要**安装Node.js环境**，安装过程中会**自动配置环境变量**
* 可以**通过终端命令**node js文件的方式来载入和执行对应的js文件:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17436855570004pc1qr.png)
