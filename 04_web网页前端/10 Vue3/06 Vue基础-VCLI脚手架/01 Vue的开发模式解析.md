目前我们使用vue的过程都是在html文件中，通过<mark class="hltr-orange">template编写自己的模板、脚本逻辑、样式</mark>等。 

**但是随着项目越来越复杂，我们会采用组件化的方式来进行开发：** 

* 这就意味着每个组件都会有自己的<mark class="hltr-orange">模板、脚本逻辑、样式</mark>等； 
* 当然我们依然可以把它们<mark class="hltr-orange">抽离到单独的js、css文件</mark>中，但是它们还是会分离开来；
* 也包括我们的script是在一个全局的作用域下，很容易出现<mark class="hltr-orange">命名冲突的问题</mark>； 
* 并且我们的代码为了适配一些浏览器，必须<mark class="hltr-orange">使用ES5的语法</mark>； 
* 在我们编写代码完成之后，依然需要<mark class="hltr-orange">通过工具对代码进行构建、代码</mark>； 


所以在真实开发中，我们可以通过一个<mark class="hltr-orange">后缀名为 .vue </mark>的<mark class="hltr-orange">single-file components (单文件组件) </mark>来解决，并且可以使用 webpack或者vite或者rollup等构建工具来对其进行处理。


# 二、单文件的特点
这个组件中我们可以获得非常多的特性： 

* 代码的高亮； 
* ES6、[[02 CommonJS和Node|CommonJS]] 的模块化能力； 
* 组件作用域的CSS； 
* 可以使用预处理器来构建更加丰富的组件，比如 TypeScript、Babel、Less、Sass等；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17461676440008e975j.png)

# 三、如何支持SFC

如果我们想要使用这一的SFC的.vue文件，比较常见的是两种方式：

* **方式一**：<mark class="hltr-orange">使用Vue CLI来创建项目</mark>，项目会默认帮助我们配置好所有的配置选项，可以在其中直接使用.vue文件； 
* **方式二**：自己<mark class="hltr-orange">使用webpack或rollup或vite这类打包工具</mark>，对其进行打包处理； 

我们最终，无论是后期我们做项目，还是在公司进行开发，<mark class="hltr-orange">通常都会采用Vue CLI的方式来完成。</mark>


