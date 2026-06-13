# 一、伪元素概括
常用的伪元素有
* `:first-line`、`::first-line`
* `:first-letter`、`::first-letter`
* `:before`、`::before`
* `:after`、`::after`

> * 上面的每列是同一种伪元素，只是不同的写法
> * 建议：伪元素使用双冒号`::`来表示，和伪类分开


# 二、::first-line 和 ::first-letter （了解）
* `::first-line`可以针对首行**文本设置**属性
* `::first-letter`可以针对首**字母设置**属性


```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            width: 500px;
            background-color: red;
            color: azure;
        }
        /* 对第一行进行设置 */
        .box::first-line {
            color: aqua;
        }
        /* 对第一个字母设置 */
        .box::first-letter {
            color: coral;
            font-size: 100px;
        }
    </style>
</head>
<body>
    <div class="box">
        建构主义学习理论是一种认知理论，强调主动学习和个人经验在知识建构过程中的重要性。该理论认为，个人通过与环境和个人经历的互动来构建自己对世界的理解和知识。建构主义学习理论的一种现实应用可以在教育领域看到，特别是基于项目的学习的使用。在基于项目的学习中，学生有机会参与现实世界的项目，这些项目要求他们积极参与材料并将所学知识应用到实际环境中。这种方法允许学生通过实践经验和协作解决问题来构建自己的知识。
    </div>
</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17147179380003q8az6.png)


# 三、::before 和 ::after (常用)
`::before`和`::after`用来在一个元素的内容之前或之后插入其他内容(可以是文字、图片)
* 常通过 content 属性来为一个元素添加修饰性的内容。

> [!tip] 注意事项
> * 在使用这个伪元素的时候 content 不要省略
> * 如果不想添加内容，只想添加一个背景为红色的正方形，`content` 内容可以编写为空
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714896920000hfuuxq.png)


当相对元素的前后添加元素的时候，这个时候可以用到 span 元素，但是代码过多的时候，每个元素都要进行 span 元素的设置，过于麻烦了。这是时候就可以使用伪元素 before 和 after 来进行设置。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box::before {
            content: "123";
            color: red;
        }

        .box::after {
            content: "abc";
            color: blue;
        }
    </style>
</head>

<body>
    <div class="box">好好学习</div>
    <div class="box">天天向上</div>
</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714897747000jpmcxs.png)

> 这样的好处就是可以定义一个 class 类型就可以对多条元素进行设置，不用每一个元素的前后都使用 span 元素来设置

但是也存在一个问题，当想对不用元素前后类型进行区别设置的时候有不好进行设置，这个就需要使用到[[08 CSS的常见选择器（selecttor）#7.1 交集选择器|交集选择器]]来进行一个区别的设置

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .item::before {
            content: "123";
            color: red;
        }
        .item::after {
            content: "abc";
            color: blue;
        }
        .new::before {
            content: "321";
            color:blue;
        }
        .new::after {
            content: "cba";
            color: blueviolet;
        }
    </style>
</head>
<body>
    <!-- 想设置不同的内容就使用不同的交集选择器 -->
    <div class="box1 item">好好学习</div>
    <div class="box2 new">天天向上</div>
</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714898464000qd1ewa.png)


> 这样在编写的时候如果想添加什么类型就选择不同的交集选择器就好了

## 3.1 运用场景
多行元素前后插入相同元素

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714895914000plh5d8.png)



