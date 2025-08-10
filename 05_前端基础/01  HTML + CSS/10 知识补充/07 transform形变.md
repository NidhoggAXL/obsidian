# 一、认识 transform
CSS transform属性允许对某一个元素进行某些形变,包括**旋转，缩放，倾斜或平移等。**

transform是形变的意思，transformer就是变形金刚

> [!tip] 注意事项
> 并非所有的盒子都可以进行transform的转换(通常行内级元素不能进行形变)
> 
> **无效的元素：**
> * 行内非替换元素：例如span、a元素等
> * table里面的元素

# 二、transform 的基本概念

**transform 属性的语法结构如下：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/172519799400073t8zc.png)

可以设置为 none 就是不进行任何的形变，或者可以设置一个`transform-list`的形变列表。- **参照语法第一排**

那这个形变列表设置就是设置一个`transform-function`形变函数。- **参照语法第三排**

```css
transform:函数名(函数值+……);
函数值可以有多个
```

形变函数可以设置多个。- **参照第五排**

```
语法解读：
<transform-function>+
+号表示一个或者多个，并且多个之间以空格分transform:scale() translate();

<box-shadow>#
#号表示一个或者多个，多个之间以，空格分隔
box-shadow:1px1px1px1px #f00;
```

**常见的函数 transform function 有：**

| 函数             | 作用  | 翻译    |
| -------------- | --- | ----- |
| translate(x,y) | 平移  | 翻译/平移 |
| scal(x,y)      | 缩放  | 规模/等级 |
| rotate(deg)    | 旋转  | 旋转    |
| skew(deg,deg)  | 倾斜  | 偏离/歪斜 |
|                |     | deg-度 |

> [!tip] 特别注意
> transform 中进行函数的形变的时候都不脱离标准流，但是会对标准流进行一个覆盖。


# 三、函数translate-位移

**平移:translate(x,y)**

* 这个CSS 函数用于移动元素在平面上的位置。
* translate本身可以表示翻译的意思，在物理上也可以表示平移

**值个数:**

* 一个值时，设置x轴上的位移
* 二个值时，设置x轴和y轴上的位移

**值类型:**

* 数字:100px
* 百分比:参照**元素本身**(refer to the size of bounding box )
	* X 轴参照的是元素的宽度
	* Y 轴参照的是元素的高度

> [!tip] 细节分化
> **细节一**：translate 和定位元素进行移动的区别
> 
> * translate 是浏览器进行渲染的时候进行移动
> * 定位元素是在结构根本上进行更改
> 
> **细节二**：translate 和[[06 position值对比|绝对定位元素]]不一样，进行了设置之后不会脱离标准流但是会覆盖在标准流上面。


**补充二**：translate是translateX和translateY函数的简写

* translate3d后续了解;

**补充三**：translate函数相对于fex布局的兼容性会好一点点

* 不过目前flex布局已经非常普及，直接使用flex布局即可:

```css
transform : translate(x,y) ;
```
# 四、函数scale-缩放

**缩放:scale(x，y)**

* scale() CSS 函数可改变元素的大小

**值个数**

* 一个值时，设置x轴上的缩放
* 二个值时，设置x轴和y轴上的缩放

**值类型:**

* 数字:
	* 1:保持不变
	* 2:放大一倍
	* 0.5:缩小一半
* 百分比:百分比不常用
* **百分比和数字都是参照与自身**

**scale函数时scaleX和scaleY的缩写**

* scale3d后续再了解;

```css
transform: scale(x,y) ;
```


# 五、函数rotate-旋转
**旋转:rotate(`<angle>`)**

**值个数**

* 一个值时，表示旋转的角度
* 使用弧度的表示法

**值类型:**

* 常用单位deg:旋转的角度(degrees)
* 正数为顺时针
* 负数为逆时针

```css
transform: rotate(数值deg) ;
```

## 5.1 rotate补充

**补充一:rotate函数是rotateZ函数的简写写法**

* rotate3d后续再了解;

**补充二:rotate的其他单位**

* 事实上rotate支持的单位是很多的,
* 度(degrees)、百分度(gradians)、弧度(radians)或数(turns);

# 六、属性transform-origin
**transform-origin:形变的原点**

* 比如在进行scale缩放或者rotate旋转时，都会有一个原点。

 **一个值:**

* 设置x轴的原点

**两个值:**

* 设置x轴和y轴的原点

**必须是`<length>`，`<percentage>`，或left, center, right, top, bottom关键字中的一个**

* left, center, right, top, bottom关键字
* length:从左上角开始计算（依据X和Y轴具体的值）
* 百分比:**参考元素本身大小**


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725267722000ftviaq.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725267739000qxsxdj.png)

# 七、函数skew-倾斜
**倾斜:skew(x，y)**

* 函数定义了一个元素在二维平面上的倾斜转换。

**值个数**

* 一个值时，表示x轴上的倾斜
* 二个值时，表示x轴和y轴上的倾斜

**值类型:**

* deg:倾斜的角度
* 正数为顺时针
* 负数为逆时针

**注意:倾斜的原点受transform-origin的影响**


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725268827000za73ad.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1725268836000j2ld55.png)

