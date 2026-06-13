# 一、一个完整HTML代码的框架

**文档类型声明：声明HTML的版本和当前的文件类型**

document-文档

type-类型

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710489446000r5p4py.png)

**标题**

```html
<h1>内容</h1>  一级标题
<h2>内容</h2>  二级标题
……
最多到h6
```

**段落**

```html
<p>内容</p>
```

**头：**

```html
<head> 元数据(metadata) </head>
例如：<title> 我的网页 </title>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710254755000kcqwww.png)


**整体**

```html
<html>
	<head> 元数据(metadata) </head>
		例如：<title> 我的网页 </title>
	<body>
		内容
	</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710254412000cckbmd.png)

**注释：**

```html
<!--注释内容-->
快捷键；ctrl+/
```

**元素表：**
https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element

# 二、元素的组成

元素：前标签-内容-后标签

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710338128000rxamth.png)

# 三、元素的属性的构造

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710338170000zn350d.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <style>
    .title {
      color:red;
    }
  </style>
</head>
<body>
  <!--<h1 属性名="属性值">我是标题</h1>-->
  <h1 class="title">我是标题</h1>
  <h1>我也是标题</h1>

  <!--超链接-->
  <a href="http://www.baidu.com">百度一下</a>
</body>
</html>
```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710339451000m1hy1d.png)

