# 一、什么是选择器（selecttor）
开发中经常需要找到特定的网页元素进行设置样式口

思考:如何找到特定的那个元素?

什么是CSS选择器

* 按照一定的规则选出符合条件的元素，为之添加CSS样式

选择器的种类繁多，大概可以这么归类

* 通用选择器 (universal selector)
* 元素选择器 (type selectors)
* 类选择器 (class selectors)
* id选择器 (id selectors)
* 属性选择器 (attribute selectors)
* 组合 (combinators)
* 伪类 (pseudo-classes)
* 伪元素 (pseudo-elements)
# 二、通用选择器 (universal selector)
通用选择器(universal selector)
* 所有的元素都会被选中;

一般用来给所有元素作一些通用性的设置
* 比如内边距、外边距;
* 比如重置一些内容;

**效率比较低，尽量不要使用;**

通用选择器会对所有的元素都进行选择，包括 HTML 和 BODY 。虽然有些浏览器会对他进行一定的优化，但是都不建议使用。

使用`*`号来进行选择，许多编程语言也使用星号来表示一种**通配符**（对所有都进行匹配）
```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

       * {

        background-color: red;

       }

    </style>

</head>

<body>

    <div>

        dajs <div>jfalsjfdlk</div>lkdfk

    </div>

    <div class="box">我是div <span>dlsajl</span>跨级元素</div>

</body>

</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17146414160009z9l17.png)

# 三、元素选择器 (type selectors)
简单选择器是开发中用的最多的选择器:
* 元素选择器(type selectors)，使用元素的名称
* 类选择器(class selectors),使用.类名
* id选择器(id selectors),使用 `#id`;

```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

        /* 元素选择器 */

        div {

            color: red;

        }

  

        /* 类选择器 */

        .box {

            color: blue;

        }

  

        /* id选择器 */

        #home {

            color: aqua;

        }

    </style>

</head>

<body>

    <div>我是div1</div>

    <div class="box">我是div2</div>

    <div id="home">我是div3</div>

</body>

</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714642268000snd0os.png)


## 2.1 id 注意事项
一个HTML文档里面的id值是唯一的，不能重复
* id值如果由多个单词组成，单词之间可以用**中划线-、下划线 **连接，也可以使用**驼峰标识**
* 最好不要用标签名作为id值

* 中划线又叫**连字符(hyphen)**

# 四、属性选择器 (attribute selectors)-了解
语法如下：
* 对同一个属性进行设置 `[att]`
* 对同一个属性的不同元素`[att=属性名]`


**其他了解的(不用记)**
* `[attr*=val]`:属性值包含某一个值val;
* `[attr^=val]`: 属性值以val开头;
* `[attr$=val]`: 属性值以val结尾:
* `[attr|=val]`:属性值等于val或者以val开头后面紧跟连接符-;
* `[attr~=val]`:属性值包含val,如果有其他值必须以空格和val分割;

```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

        /* 对相同属性进行设置 */

        [title] {

            color: red;

        }

  

        /* 对相同属性不同元素进行设置 */

        [title=div] {

            background-color: blue;

        }

    </style>

</head>

<body>

    <!-- title 是全局属性 -->

    <div>我是div元素</div>

    <div title="div">我也是div元素</div>

    <p>我是p元素</p>

    <h2 title="h2">我是h2元素</h2>

</body>

</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714654967000h4s3ha.png)

> 在开发中很少使用


# 五、后代选择器（descendant combinator）
## 5.1 所有的后代(直接/间接的后代)
**选择器之间以空格分割**

**举例：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17146556160007gecpe.png)

把 `div.hone` 树下的所有 `span` 进行设置
```html
    <style>

        /* 后代选择器 */

        .home span {

            color: red;

            font-size: 30px;

        }

    </style>
```

> [!tip] 特别注意
> 在使用后代选择器的时候`home`后面要增加一个**空格**在编写`span`,如果不加空格的话就是另一个选择器组-交集选择器

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17146559000003b6fyb.png)

## 5.2 直接子代选择器(必须是直接子代)
**选择器之间以 `>` 分割;**

> [!tip] 什么是直接子代
> 父亲的下一代就是直接子代
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17146556160007gecpe.png)
> 如上的`div.box`和`div.content`就是直接子代

代码示例：
```html
    <style>

        /* 直接自带选择器 */

        .home > box {

            background-color: blue;

        }

    </style>
```

# 六、兄弟选择器（sibling combinator）- 理解
> [!tip] 兄弟定义
> 同意层的元素之间互为兄弟
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17146572420004lekgp.png)
> * box 和 content互为相邻兄弟
> * box 和  content 、long、ao 为全兄弟

## 6.1 相邻兄弟选择器
**使用 + 链接**
```html
    <style>

        /* 相邻兄弟选择器 */

        .box + div {

            /* 等同与 .box + .content */

            background-color: red;

        }

    </style>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171465756100049wn0k.png)


## 6.2 全兄弟选择器
**使用`~`链接**

```html
    <style>

        .box ~ div {

            color:red;

        }

    </style>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171465772800065cljh.png)

## 6.3 小结
* 兄弟选择器只能向下
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714659841000kvy2s1.png)
> 如果是对类 box 进行兄弟选择器进行选择的时候，只能选择 box 代码以下的兄弟，对 box 上面的 div 是不起作用的。


# 七、选择器组
## 7.1 交集选择器
**交集选择器**: 需要同时符合两个选择器条件(两个选择器紧密连接)
* 在开发中通常为了精准的选择某一个元素,

举例：
对同为 box 的类只对 div 进行设置（div 有两个类名）
```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

        /* div和点之间不要加空格，加了就是后代选择器*/

        div.content {

            font-size: 40px;

            color: red;

        }

    </style>

</head>

<body>

    <div class="box content">我是div元素</div>

    <p class="box">我是p元素</p>

</body>

</html>
```

> [!tip] 特别注意
> div和点之间不要加空格，加了就是后代选择器

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714658615000eve321.png)

## 7.2 并集选择器
**井集选择器**:符合一个选择器条件即可(两个选择器以,号分割)
* 在开发中通常为了给多个元素设置相同的样式

**举例：**
对 body 中的全部属性进行设置
```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

        /* 等价与 .box,.p,.ao,.miao*/

        div,p,span,h1 {

            font-size: 30px;

            color: red;

        }

  
  

    </style>

</head>

<body>

    <div class="box">哈哈哈</div>

    <p class=content">呵呵呵</p>

    <span class="ao">嘻嘻</span>

    <h1 class="miao">嗷嗷哦</h1>

</body>

</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714659491000dspnhb.png)

* 类型设置也可以编写成如下代码
```html
    <style>

        .box,.ao,.miao,.content {

            font-size: 30px;

            color: red;

        }

    </style>
```




