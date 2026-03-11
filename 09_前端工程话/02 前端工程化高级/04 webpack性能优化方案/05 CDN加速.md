# 一、什么是CDN？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773218616000wkpexd.png)

# 二、购买CDN服务器

如果所有的静态资源都想要放到CDN服务器上，我们需要购买自己的CDN服务器；

 - 目前阿里、腾讯、亚马逊、Google等都可以购买CDN服务器；
 - 我们可以直接修改publicPath，在打包时添加上自己的CDN地址；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773218724000bbu9e9.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773218728000coh1gl.png)

# 三、第三方库的CDN服务器

通常一些比较出名的开源框架都会将打包后的源码放到一些比较出名的、免费的CDN服务器上：

 - 国际上使用比较多的是unpkg、JSDelivr、cdnjs；
 - 国内也有一个比较好用的CDN是bootcdn；

在项目中，我们如何去引入这些CDN呢？

 - 第一，在打包的时候我们不再需要对类似于lodash或者dayjs这些库进行打包；
 - 第二，在html模块中，我们需要自己加入对应的CDN服务器地址；

第一步，我们可以通过webpack配置，来排除一些库的打包：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773219246000hzeyz8.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17732194330007nj2c5.png)


第二步，**在html模块中**，加入CDN服务器地址：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773219251000xhycue.png)

