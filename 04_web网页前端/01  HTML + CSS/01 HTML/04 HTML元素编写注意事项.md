# 一、块级元素、inline-block元素
一般情况下，可以**包含其他任何元素**(比如块级元素、行内级元素、inline-block元素)

**特殊情况**，p元素不能包含其他块级元素

**如果p元素里面包含了块级元素，侧浏览器在解析的时候出现错乱：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714920704000dohvvw.png)



# 二、行内级元素(比如a、span、strong等)
一般情况下，行内积元素只能包含行内级元素，不要包含块级元素

下面这种行内级元素里面包含块级元素就是垃圾：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1714920836000hwvz3u.png)



