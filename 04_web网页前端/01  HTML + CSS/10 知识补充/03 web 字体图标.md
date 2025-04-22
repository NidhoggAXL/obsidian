# 一、Web 字体图标

**字体图标的好处:**

* 放大不会失真
* 可以任意切换颜色
* 用到很多个图标时，文件相对图片较小

**字体图标的使用:**

* 登录阿里icons(https://www,iconfont.cn/)
* 下载代码，并且拷贝到项目中

**将字体文件和默认的css文件导入到项目中**

**字体图标的使用有好几种办法：**

**直接通过内容（字符实体），怎么找到这个[[01_字符实体|字符实体]]呢？**

* 在下载的文件里面有一个  .html 点击一下跳转到网页就可以找到

```html
<body>
	<i class="iconfont">&#xe795;</i>
</body>
```

**不通过字符实体，使用[[10 伪元素（pseudo-elements）|伪元素]]**

 * 这个内容也不是随便添加的，在下载的文件 css 里面就可以找到内容是什么![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723097086000k1ruyr.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17230971190006uhygk.png)



**总结一下字体图标的使用（实际开发中）：**

1. 首相需要去下载一个字体图标，一般下载的图标文件不会只是一个。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17230959630001s85qj.png)

2. 把字体图标文件中的 .fft 和 .css 放入到web项目的文件夹中。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723096068000pw6hia.png)

3. 在 web 的结构 html 中引用这个文件夹中的文件 .css

* 不过这里需要注意你下载文件的 .css 中的 clsss ，方便后面对需要使用的字体图标添加正确的 class 。

4. 使用不通过字符实体的方式进行字体图标的使用。

