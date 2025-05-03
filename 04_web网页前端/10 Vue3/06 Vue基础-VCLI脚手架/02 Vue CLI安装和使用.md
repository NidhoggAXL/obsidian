# 一、Vue CLI脚手架
**什么是Vue脚手架？** 

* 我们前面学习了如何通过webpack配置Vue的开发环境，但是在真实开发中我们不可能每一个项目从头来完成所有的 webpack配置，这样显示开发的效率会大大的降低； 
* 所以在真实开发中，我们通常会使用<mark class="hltr-orange">脚手架</mark>来创建一个项目，Vue的项目我们使用的就是<mark class="hltr-orange">Vue的脚手架</mark>； 
* 脚手架其实是建筑工程中的一个概念，在我们软件工程中也会将一些<mark class="hltr-orange">帮助我们搭建项目的工具称之为脚手架</mark>；
* <mark class="hltr-orange">Vue的脚手架里面已经默认集成了 webpack 了.</mark>

**Vue的脚手架就是Vue CLI：** 

* CLI是<mark class="hltr-orange">Command-Line Interface,</mark> 翻译为<mark class="hltr-orange">命令行界面</mark>； 
* 我们可以通过CLI<mark class="hltr-orange">选择项目的配置和创建</mark>出我们的项目； 
* Vue CLI已经<mark class="hltr-orange">内置了webpack相关的配置</mark>，我们不需要从零来配置；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17461701150007sqb49.png)

# 二、Vue CLI安装和使用

**安装Vue CLI**

* 我们是进行全局安装，这样在任何时候都可以通过vue的命令来创建项目；

```
npm install @vue/cli -g
```

**升级Vue CLI：** 

* 如果是比较旧的版本，可以通过下面的命令来升级

```
npm update @vue/cli -g
```

**通过Vue的命令来创建项目**

```
Vue create 项目的名称
```

# 三、Vue create 项目的过程

**第一次创建vue的项目为显示是否使用国内的镜像源：**

* 一般国内都是使用淘宝的源
* 看习惯选择

后面就会进行vue项目初始化的界面选择：

1. 选择使用那一个vue版本或者自定义选择特性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746171100000a5jmag.png)

2. 如果选择特性就会有如下的选项，按住空格选择一个，a选择全部

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746171222000kcpsfh.png)

3. 选择特性后再选择vue的版本

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17461712640002h0z3d.png)

4. 放置配置的信息（一般选择放到独立的文件中，这样方便后期的管理）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17461713450003v1bya.png)

