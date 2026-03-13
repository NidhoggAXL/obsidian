# 一、认识shimming

shimming是一个概念，是某一类功能的统称：

 - shimming翻译过来我们称之为 垫片，相当于给我们的代码填充一些垫片来处理一些问题；
 - 比如我们现在依赖一个第三方的库，这个第三方的库本身依赖lodash，但是默认没有对lodash进行导入（认为全局存在
lodash），那么我们就可以通过ProvidePlugin来实现shimming的效果；

注意：webpack并不推荐随意的使用shimming

 - Webpack背后的整个理念是使前端开发更加模块化；
 - 也就是说，需要编写具有封闭性的、不存在隐含依赖（比如全局变量）的彼此隔离的模块；

# 二、Shimming预支全局变量

目前我们的lodash、dayjs都使用了CDN进行引入，所以相当于在全局是可以使用_和dayjs的

假如一个文件中我们使用了axios，但是没有对它进行引入，那么下面的代码是会报错的；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773221384000ss6f6n.png)


我们可以通过使用ProvidePlugin来实现shimming的效果：

 - ProvidePlugin能够帮助我们在每个模块中，通过一个变量来获取一个package；
 - 如果webpack看到这个模块，它将在最终的bundle中引入这个模块；
 - 另外ProvidePlugin是webpack默认的一个插件，所以不需要专门导入；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17732214120002aesm3.png)

这段代码的本质是告诉webpack：

 - 如果你遇到了至少一处用到 axios变量的模块实例，那请你将 axios package 引入进来，并将其提供给需要用到它的模块。
