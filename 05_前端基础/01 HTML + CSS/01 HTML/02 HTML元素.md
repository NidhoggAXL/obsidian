这里的html元素和HTML元素的区别：
* 大写的HTML元素表示的是HTML语言下面的所有元素
* 小写的html元素表示的是html里面的 `h1/p/img` 之类的元素

# 一、head元素

**HTML head 元素 规定文档相关的配置信息(也称之为元数据)，包括文档的标题，引用的文档样式和脚本等。**

* 什么是元数据(meta data)，是描述数据的数据;
* 这里我们可以理解成对**整个页面的配置**:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1717679675000l3ppl9.png)

**常见的设置有哪些呢?一般会至少包含如下2个设置。**

**网页标题**：title 元素 title-名称

```html
<title>网页标题</title>
```

**网页的编码**:meta元素  meta-元语言

* 可以用于设置网页的字符编码，让浏览器更精准地显示每一个文字，不设置或者设置错误会导致乱码
* 一般都使用 utf-8 编码，涵盖了世界上几乎所有的文字;

# 三、body常见元素

对页面的描述，页面超文本编写的地方。

# 四、h元素

在一个页面中通常会有一些比较重要的文字作为标题，这个时候可以使用h元素。

`<h1>-<h6>`标题(Heading) 元素呈现了六个不同的级别的标题

* `Heading`是头部的意思，通常会用来做标题口
* `<h1>`级别最高，而`<h6>`级别最低。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1717679935000h0j0d2.png)


> [!tip] 注意:
> h标签通常和[[元素语义化及SEO|SEO]]优化有关系

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710493884000vg4z3y.png)

那么浏览器是通过什么来进行区分h1~h6的呢（呈现的时候）？

> [!note]
> 是通过CSS来进行渲染的，h标签告诉是什么标题，CSS在对不同的标题进行不同的渲染。
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710494865000ot1m0a.png)
> 
> CSS会对不同标签进行区域内容的不同设置，例如：字体大小、颜色，上下间距等。

# 五、P元素

如果想表示一个段落，这个时候可以使用p元素。

HTML`<p>`元素(或者说 HTML 段落元素)表示文本的一个段落

* p 元素是paragraph单词的缩写，是段落、分段的意思;
* p 元素多个段落之间会有一定的间距

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17176800360005gxz18.png)


```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <p>
    以广东为例，2020年广东提出要发展十大战略性支柱产业集群，培育十大战略性新兴产业集群。十大战略性支柱产业集群包括新一代电子信息、绿色石化等等，十大战略性新兴产业集群包括半导体与集成电路、高端装备制造等等。广东拥有全国最大、产业链最完整的新一代电子信息产业集群，在全球也有重要位置。
  </p>

  <p>
    央视网消息：2019年，我国提出要把粤港澳大湾区打造成为“具有全球影响力的国际科创中心”。  在世界知识产权组织（WIPO）发布的《2023年全球创新指数》中，全球顶级科技创新集群的排名，前五名中中国有三地上榜。北京位居第四，“上海—苏州”区域位居第五，“深圳—香港—广州”区域位居全球第二！这已经是它在这个排名中连续第四年位列全球第二，可见这一区域在科创方面的实力和国际影响力。
  </p>
</body>

</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710495534000v1dmmi.png)

# 六、img元素

那么应该如何告诉浏览器来显示一张图片呢?使用img元素。

HTML `<img>`元素将一份图像嵌入文档.

* img是image单词的所以，是图像、图像的意思;
* 事实上img是一个**可替换元素(replaced element)**;


**img有两个常见的属性:**

 - `src`属性:source单词的缩写，表示源
	 - 是必须的，它包含了你想嵌入的图片的文件路径
 - `alt`属性:不是强制性的，有两个作用
	 * **作用一**:当图片加载不成功(错误的地址或者图片资源不存在)，那么会显示这段文本;
	 * **作用二**:屏幕阅读器会将这些描述读给需要使用阅读器的使用者听，让他们知道图像的含义;

**img的实现方法**：使用img占据网页的一些空间

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171050642600003zug2.png)

在这个空间里面使用src找到图片的源路径->同源可以去服务器上面找到图片->在网页里面用这个替换img占据的空间，如果没有找到图片，那么浏览器就回自动添加一个图片缺少的提示图表。

**所以img也叫可替换元素。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171050619400071ayp4.png)

## 6.1 src属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17105065080004hwy0m.png)

## 6.2 alt属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171050653700070w29n.png)

## 6.3 img元素中的图片路径

**设置img的src时，需要给图片设置路径:**

* 网络图片:一个URL地址(后续会专门讲URL)
	* 网络图片的设置非常简单，给一个地址即可口本地图片:
* 本地电脑上的图片，后续会和htmI一起部署到服务;

**本地图片的路径有两种方式:**

* 方式一:绝对路径(几乎不用);
	* 从电脑的根目录开始一直找到资源的路径，![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17176804250006yuydl.png)
* 方式二:相对路径(常用);![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1717680497000h3tjng.png)
	* 相当于当前文件的一个路径;
	* `.`代表当前文件夹(1个.)，**可以省略**
	* `..`代表上级文件夹(2个.)

> [!tip]
> 
> 对于网页来说，不管什么操作系统(Windows、Mac、Linux)，路径分隔符都是`/`（斜杆），而不是`\`（反斜杆）


```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <!-- 1.网络图片：使用网络链接 -->
  <h1>网络图片</h1>
  <img src="https://k.sinaimg.cn/n/sinacn10111/300/w1728h972/20190920/89b2-iewtemz5328342.jpg/w700d1q75cms.jpg" alt="雷姆图片">
  <hr/>

  <h1>本地图片</h1>
  <h2>绝对路径图片</h2>
  <img src="D:\cod\web\imgs\xiaodao.jpg" alt="xiaodao">

  <h2>相对路径图片</h2>
  <img src="../imgs/xiyang.jpg" alt="xiyang">
</body>

</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17105088790003fucgq.png)


# 七、a元素

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710574815000p8sdzw.png)

> [!tip] 
>  reference-引用
 > blank-空白的
 > target-目标
 
## 7.1 target

**当不对target进行属性设置的时候回默认为_self。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710575386000rq2su3.png)

> [!tip]
> 
> 同时可以看出来，target没有定义时是自动默认为_self的。


 **target属性值设置为_blank时。为在创建一个空白的网页，在这个网页中跳转到百度**
 ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710575612000mme6v6.png)

## 7.2 a元素跳转到网页中的具体位置

**锚点链接可以实现:跳转到网页中的具体位置**

**锚点链接有两个重要步骤:**

* 在要跳到的元素上定义一个id属性
* 定义a元素，并且a元素的href指向对应的id:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1717680777000fj7hq6.png)


### 7.2.1 文本链接

**对sheme进行id属性的设置，a标签里面使用`#`来知道要跳转的地方**

文本->文本:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710577652000wxb5nb.png)

文本->图片:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <a href="#leimu">雷姆照片</a>
  <p>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br>
  </p>

  <img src="../imgs/leimu.jpg" alt="" id="leimu">
</body>
</html>
```

### 7.2.2 图片链接

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710578612000ljz87u.png)

图片->图片:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <a href="#leimu">
    <img src="../imgs/xiaodao.jpg" alt="">
  </a>
  <p>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
  </p>

  <img src="../imgs/leimu.jpg" alt="" id="leimu">
</body>
</html>
```

 图片->地址：
 
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <h1>雷姆的图片超链接</h1>
  <a href="https://www.baidu.com/from=844b/ssid=0/s?word=%E9%9B%B7%E5%A7%86%E5%9B%BE%E7%89%87%E5%A3%81%E7%BA%B8%E8%B6%85%E6%B8%85&sa=re_dl_prs_34689_4&ms=1&rqid=7069369201125033412&rq=NIKE%E8%B6%85%E6%B8%85%E5%A3%81%E7%BA%B8&rsf=68040014&asctag=13544" target="_blank">
    <img src="https://k.sinaimg.cn/n/sinacn10111/269/w1200h669/20190920/2b21-iewtemz5328511.jpg/w700d1q75cms.jpg" alt="">
  </a>
</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710578459000iqpoai.png)

## 7.3 a元素的其他URL

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17105808670002rbfn5.png)

a 元素也可以来发送邮箱和下载数据，发送到指定的邮箱里面。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <a href="aoao.zip">下载zip压缩包</a>
  <a href="mailto:1234@qq.com">发邮件给1234</a>
</body>
</html>
```

## 7.4 iframe元素

利用iframe元素可以实现:在一个HTML文档中嵌入其他HTML文档

**frameborder属性**

* 用于规定是否显示边框
	* `1`:显示
	* `0`:不显示
* 其中给的窗口大概率都是小的，会在这个窗口中显示滑动方便浏览嵌套的网页

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710588248000bffhgb.png)

> [!tip]
> 
> 可以看到有一些网页是不允许被嵌套的。

# 八、iframe和a元素的结合使用

**a元素target的其他值:**

* `_parent`:在父窗口中打开URL
* `_top`:在顶层窗口中打开URL

## 8.1`_parent`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710589170000hwaehn.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710589196000531l9m.png)

`target="_parent"`表示的是在父及打卡，这里使用了嵌套，所以在点击打开淘宝时，实在父级打开的。

## 8.2 `_top`

**多级嵌套**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710589854000pfvc1v.png)

> [!tip]
> 
> 直接是打开最外面的嵌套

# 九、div元素、span元素

**div元素、span元素的历史：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710590672000ig424a.png)

**div元素、span元素的区别：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171059081500085575o.png)

**div元素、span元素的使用：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .area{
      border: 1px solid red;
    }
    .keyword{
      font-size: 30px;
      font-weight: 700;
      color:blue;
    }
  </style>
</head>

<body>
  <h1>学习前端</h1>
  <div class="area">
  <h3>1. HTML+CSS的学习</h3>
    <p>
      先学习HTML，后面在学习CSS
    </p>
  </div>
  <div class="area">
    <h3>2. JavaScript的学习</h3>
    <p>
      深入的学习<span class="keyword">JavaScript</span>的学习
    </p>
  </div>
  <div class="area"
    <h3>3. 学习一些开发工具的使用</h3>
      <p>
        对好多的开发工具要学习。
      </p>
  </div>
</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710592239000nx1qdp.png)

**这里是希望JavaScript这个重点标识不独自占据一行，所以是使用span而不是div，使用div的话JavaScript会独自占据一行。**

# 十、不常用元素

**strong元素:内容加粗、强调:**

* 通常加粗会使用css样式来完成:
* 开发中很偶尔会使用一下;

**i元素:内容倾斜;**

* 通常斜体会使用css样式来完成;
* 开发中偶尔会用它来做字体图标(因为看起来像是icon的缩写)

**code元素:用于显示代码**

* 偶尔会使用用来显示等宽字体

**br元素:换行元素**

* 开发中已经不使用:

**更多元素详解，查看MDN文档**

* https://developer.mozilla.org/zh-CN/docs/eb/HTML/Element


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710594060000wt40xo.png)


# 十一、HTML全局属性

**我们发现某些属性只能设置在特定的元素中**

* 比如img元素的src、a元素的href;

**也有一些属性是所有HTML都可以设置和拥有的，这样的属性我们称之为“全局属性(Global Attributes)**

* 全局属性有很多:https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global.attributes

**常见的全局属性如下:**

* `id`:定义唯一标识符(ID)，该标识符在整个文档中必须是唯一的。其目的是在链接(使用片段标识符)，脚本或样式(使用 CSS)时标识元素。
* `class`:一个以空格分隔的元素的类名(classes)列表，它允许CSS和Javascript 通过类选择器或者DOM方法来选择和访问特定的元素;
* `style`:给元素添加内联样式;
* `title`:包含表示与其所属元素相关信息的文本。 这些信息通常可以作为提示呈现给用户，但不是必须的。
	* 在鼠标移动到元素上面2秒中后，就会显示出来。


## 11.1 title 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <p title="啊哈哈哈">我是一个CoderL</p>
</body>
</html>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1710595930000k8e2ln.png)


