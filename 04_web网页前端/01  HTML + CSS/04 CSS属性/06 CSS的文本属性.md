# text-decoration(常用)
> decoration-装饰、装修

a元素默认添加下划线(underline):

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711547167000p8tp0v.png)

自己添加下滑线：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711547386000a1sskq.png)

添加其他的滑线：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17115487170003ek0li.png)

取消下滑想：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711548798000cmoyd3.png)



# text-transform(一般)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17116070740006zw4gc.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17116072970007q68q3.png)

# text-indent(一般)

text-indent用于设置第一行内容的缩进

text-indent: 2em;刚好是缩进父元素`font-size:;`的两倍大小。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711608164000dr2ij3.png)



# text-align(重要)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171160989400027o556.png)


**文本对齐：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17116091380007chdrs.png)

**图片对齐：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711609291000h1ey7p.png)

**块对齐：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711610170000o1hvvq.png)

会发现虽然设置了box的`test-align: center;`但是并没有进行居中对齐的方式，因为W3C里面已经写了只对行内级元素有效。

> [!tip] test-align的行内级`(inline-level)`
> div是一个块级，`test-align`只对`inline-level`的元素有用，对于块级并没有什么作用。

那如何改变呢？看下面的代码：改变div的特性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711610579000fi0jor.png)

## justify
在div中当没有进行设置的时候是默认left对齐的。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711611953000yrn2gk.png)

当进行justify设置时：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711611996000d4h92i.png)

> 但是这里可以看出最后一排是没有进行设置，可以理解为网页出现是代替报纸的，报纸的格式是左对齐，方便给人们阅读。但是要更改也是可以的
> ```html
> text - align - last : justify;
> ```
> 这样最后一行也就可以进行设置了。



# word/letter-spacing(了解)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711612790000lyqc9l.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1711612746000go65qd.png)
