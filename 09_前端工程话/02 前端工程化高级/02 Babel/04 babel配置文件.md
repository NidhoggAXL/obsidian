
像之前一样，我们可以将babel的配置信息放到一个独立的文件中，babel给我们提供了两种配置文件的编写：

 - `babel.config.json`（或者.js，.cjs，.mjs）文件；
 - `.babelrc.json`（或者.babelrc，.js，.cjs，.mjs）文件；

它们两个有什么区别呢？目前很多的项目都采用了多包管理的方式（babel本身、element-plus、umi等）；

 - `.babelrc.json`：早期使用较多的配置方式，但是对于配置Monorepos项目是比较麻烦的；
 - `babel.config.json`（babel7）：可以直接作用于**Monorepos项目的子包，更加推荐**；


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17729817650000ch2nb.png)


