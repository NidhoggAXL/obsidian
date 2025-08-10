# 一、CSS编写的痛点
CSS作为一种样式语言，本身用来给HTML元素添加样式是没有问题

但是目前前端项目已经越来越复杂,不再是简简单单的几行CSS就可以搞定的,我们需要几千行甚至上万行的CSS来完成页面的美化工作,

随着代码量的增加,必然会造成很多的编写不便:

* 比如大量的重复代码,虽然可以用**类来勉强管理和抽取**,但是使用起来依然不方便;
* 比如**无法定义变量(当然目前已经支持)**,如果一个值被修改,那么需要**修改大量代码, 可维护性很差;(比如主题颜色)**
* 比如没有专门的作用域和嵌套,**需要定义大量的id/class来保证选择器的准确性,**避免样式混淆;
* 等等一系列的问题;

所以有一种对CSS称呼是“面向命名编程”

社区为了解决CSS面临的大量问题,出现了一系列的CSS预处理器(CSS preprocessor)

* CSS 预处理器是一个能让你通过预处理器**自己独有的语法来生成CSS的程序;**
* 市面上有很多css预处理器可供选择，且绝大多数CSS预处理器会**增加一些原生CSS不具备的特性**
* 代码最**终会转化为css来运行**,因为对于**浏览器来说只识别css;**

# 二、常见CSS预处理器
**目前使用较多的是三种预处理器:**

Sass/Scss:

* 2007年诞生，最早也是最成熟的CSS预处理器，拥有ruby社区的支持，是属于Haml(一种模板系统)的一部分;
* 目前受LESS影响，已经进化到了**全面兼容CSS的SCSSm**

Less:

* 2009年出现，受SASS的影响较大，但又**使用CSS的语法**，让大部分**开发者更容易上手;**
* 比起SASS来，可编程功能不够，不过优点是使用方式简单、便捷，兼容CSS，并且已经足够使用;
* 另外反过来也影响了SASS演变到了SCSS的时代;
* 著名的Twitter Bootstrap就是采用LESS做底层语言的，也包括React的Ul框架AntDesign。

Stylus:

* 2010年产生，来自Nodejs社区，主要用来给Node项目进行CSS预处理支持;
* 语法偏向于Python,使用率相对于Sass/Less少很多

# 三、Less

## 3.1 认识Less

什么是Less呢?我们来看一下官方的介绍:
* It's CSS, with just a little more.
* 这就是CSS，只是在多了一点东西。

Less(Leaner Style Sheets 的缩写)是一门CSS 扩展语言,并且兼容CSS。

* Less增加了很多**相比于CSS更好用的特性;**
* 比如**定义变量、混入、嵌套、计算**等等;
* **Less最终需要被编译成CSS运行于浏览器中(包括部署到服务器中);**

## 3.2 Less代码的编译

这段代码如何被编译成CSS代码运行呢?

**方式一**:下载Node环境，通过npm包管理下载less工具，使用less工具对代码进行编译;

* 因为目前我们还没有学习过Node，更没有学习过npm工具;
* 所以先阶段不推荐大家使用less本地工具来管理;
* 后续我们学习了webpack其实可以自动完成这些操作的:

**方法二**：通过VSCode插件来编译成CSS或者在线编译

* 插件：easy less插件来自动生成，不过会多出一个css文件
* 在线编译：https://esscss.org/less-preview/

**方式三**:引入CDN的less编译代码，对less进行实时的处理;

```html
<link rel="stylesheet/less" href="./less/demo.less">
<script src="https://cdn.jsdelivr.net/npm/less@4" ></script>
```

js 是从网络先下载到本地的，在进行使用，这样的话每次使用的时候都要从网络下载，**效率会比较低一点**。

**方式四**:将less编译的js代码下载到本地，执行js代码对less进行编译;

```html
<link rel="stylesheet/less" href="./less/demo.less">
<script src="./js/js_demo.js" ></script>
```

创建一个 js 的文件，把代码从网络中下载下来到本地，使用的时候连接本地就可以啦，**这样效率会高一点**。

## 3.3 Less的语法

### 3.3.1 Less基本语法

**less完全兼容CSS**：在less文件里面可以之间编写成CSS的编写方式。

**less支持定义变量**：后续在使用变量的时候，如果要修改值，之间修改定义变量的值就好。

**less支持嵌套**：让代码编写的更加有层次性。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/172663678500034vq8c.png)

**特殊符号:& 表示当前选择器的父级**

例如一个元素处于hover状态下不同的样式：

```less
.container {
	.box {
		color: red;
	}
	.box:hover {
		color: blue;
	}
}
```

> 上面编写虽然也是可以的，但是很明显 box的 hover转换应该是和hover一起进行设置，前面使用css编写时没有办法，现在使用less编写了，应该是要可以写进去的。

```less
.container {
    .box {
        color: red;
        &:hover {
            color: blue;
        }
    }
}
```

> 这里面就使用了 & 符号，表示选择器的父级，就是 box了，这样就可以在同一个 box 选择器里面进行设置了。

### 3.3.2 运算（operations）- 了解
在Less中，算术运算符` +、-、*、/`可以对任何数字、颜色或变量进行运算。

* 算术运算符在加、减或比较之前会进行单位换算，计算的结果**以最左侧操作数的单位类型为准**;
* 如果单位换算无效或失去意义，则忽略单位:

```less
.box {
    width: 10% + 50px;
    background-color: #f00+#0f0;
}
```

### 3.3.3 混合或混入（mixins）
在原来的CSS编写过程中，多个选择器中可能会有大量相同的代码

* 我们希望可以将这些代码进行抽取到一个独立的地方，任何选择器都可以进行复用:
* 在less中提供了混入(Mixins)来帮助我们完成这样的操作;

混合(Mixin)是一种将一组属性从一个规则集(或混入)到另一个规则集的方法

```less
//混入
.box {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}
  
.a {
    width: 100px;
    height: 200px;
    color: #333;
    .box();
}
```

这样的话把 box 混入到 a 里面，这样就不需要再在 a 后面添加一个 box 的类，减少了类的重复代码。

> [!tip] 注意:
> 混入在没有参数的情况下，小括号可以省略，但是不建议这样使用

**混入传入参数：**

```less
// 混入传入参数

.mainBoder(@size:2px,@color:red) {
    boder:@seze solid @color;
}

.box {
    // 没有参数传入，使用定义的默认值
    .mainBoder();
    // 有参数传入，使用参数
    .mainBoder(1px,blue);
}
```

### 3.3.4 混入和映射结合
```less
//混入和映射结合使用
.boxsize {
    width: 100px;
    height: 100px;
}

.box {
    //大括号里面时需要映射得到的属性
    width: .boxsize()[width];
}
```

这样的好处是，解决了less不能随意自定义函数的缺陷。

### 3.3.5 less其他语法补充-了解
**extend继承：**

* 和mixins作用类似，用于复用代码
* 和mixins相比，继承代码最终会转化成并集选择器

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726648795000c6ffkc.png)

**Less内置函数：**

* Less 内置了多种函数用于转换颜色、处理字符串、算术运算等。
* 内置函数手册:https://less.bootcss.com/functions/

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726648822000rjnirb.png)


**作用域(Scope)：**

* 在查找一个变量时，**首先在本地查找变量和混合(mixins)**
* 如果找不到，**则从“父”级作用域继承**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726649050000xzz1wh.png)


**导入(Importing)：**

* 导入的方式和CSS的用法是一致的;
* 导入一个 .less 文件，此文件中的所有变量就可以全部使用了
* 如果导入的文件是 **.less 扩展名**，则可以将**扩展名省略掉;**

# 四、Sass和Scss(基础了解)

事实上，最初Sass 是Haml的一部分，Haml是一种模板系统，由 Ruby开发者设计和开发

所以，Sass的语法使用的是**类似于Ruby的语法**，**没有花括号，没有分号，具有严格的缩进**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1726649485000gbr8f4.png)

我们会发现它的语法和Css区别很大，后来官方推出了全新的语法SCSS，意思是SassyCss，他是完全兼容CSs的。

目前在前端学习SCSs直接学习SCSs即可:
* Scss的语法也包括变量、嵌套、混入、函数、操作符、作用域等;
* 通常也包括更为强大的控制语句、更灵活的函数、插值语法等;
* 可以根据之前学习的less语法来学习一些SCSs语法:
* 学习网站：https://sass-lang.com/guide

