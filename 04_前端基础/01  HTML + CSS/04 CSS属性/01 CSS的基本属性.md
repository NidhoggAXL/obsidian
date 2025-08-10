# 一、认识CSS
CSS表示层叠样式表(Cascading Style Sheet，简称:CSS，又称为又称串样式列表、级联样式表、串接样式表、阶层式样式表)是为网页添加样式的代码。

# 二、CSS的历史
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171145464200013vcwq.png)

CSS 并没有什么真正意义上面的CSS3，从2011年开始就开始对CSS2进行分模块开始更行了，各自更行自己的。

# 三、CSS编写
```
(属性：属性的值)-(属性)

```

* 声明(Declaration)一个单独的CSS规则，如color: red;用来指定添加的CSS样式。
	* 属性名(Property name) :要添加的css规则的名称;
	* 属性值(Property value):要添加的css规则的值;

# 四、CSS的样式(style)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711454955000uwumwg.png)

CSS样式之间使用;(分号)隔开，**最后面的样式推荐也使用**

## 4.1 内联样式(inline style)
line-行
```html
<!DOCTYPE html>

<html lang="en">

<head>

  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<body>

  <!-- 内联样式(inline) -->

  <!-- 1.单样式编写 -->

  <div style="font-size: 20px;">我是单样式</div>

  

  <!-- 2.多样式编写 -->

  <div style="color: red;font-size: 50px;">我是多样式</div>

</body>

</html>
```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711455564000qz4tb1.png)


## 4.2 内部样式(internal)
```html
<!DOCTYPE html>

<html lang="en">

<head>

  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

  

  <style>

    /* 内部样式(internal) */

  

    /* 定义全局div的属性 ,包括增加属性class的div*/

    /* div {

      color: brown;

      font-size: 20px;

      background-color: aqua;

    } */

  

    /* 对定义属性class的div进行样式改变 */

    .div-once {

      color: brown;

      font-size: 20px;

      background-color: aqua;

    }

  

  </style>

</head>

<body>

  <div class="div-once">我是内部样式</div>

  <div>我也是内部样式</div>

  

</body>

</html>
```

**在Vue的开发过程中，每个组件也会有一个style元素，和内部样式表非常的相似（原理并不相同);**

## 4.3 外部样式
### 4.3.1 引入外部一个CSS里面的样式
外部一个CSS：
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711458134000vz5ku4.png)

**在引入外部样式的时候使用link(链接；链路)单标签：**
```html
<link rel = "引入的类型" href = "引入的链接"
```

外部样式1：
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711458065000m50cdc.png)

外部样式2：
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711458108000l4o00k.png)

### 4.3.1 引入外部多个个CSS里面的样式
这个时候就需要多多个CSS的样式进行一个统一(就是和C语言里面的模块话代码一样有定义、头、源)

**头：**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711459082000k5uq6y.png)



**定义：**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711458415000c2e491.png)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17114584230006crnji.png)

**源：在里面直接引入头index.css**
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17114591130000nb6zj.png)
