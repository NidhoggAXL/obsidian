# 一、认识flex布局
## 1.1 为什么会出来flex布局(历史)

**原来布局的痛点：**

* 比如在父内容里面垂直居中一个块内容。
* 比如使容器的所有子项等分可用宽度/高度，而不管有多少宽度/高度可用。
* 比如使多列布局中的所有列采用相同的高度，即使它们包含的内容量不同。
## 1.2 什么是flex布局

**Flexbox翻译为弹性盒子:**

* 弹性盒子是一种用于**按行或按列**布局元素的**一维布局**方法
* 元素可以**膨胀以填充额外的空间**,**收缩以适应更小的空间:**
* 通常我们使用Flexbox来进行布局的方案称之为**fex布局**(flex layout);

**flex布局是目前web开发中使用最多的布局方案:**

* flex布局(Flexible 布局，弹性布局);
* 目前特别在**移动端**可以说已经完全普及;
* 在PC端也几乎已经完全普及和使用,只有**非常少数的网站依然在用浮动来布局**

**为什么需要flex布局呢?**

* 长久以来，CSS 布局中唯一可靠且跨浏览器兼容的布局工具**只有 float和 positioning.**
* 但是这两种方法本身存在很大的局限性,并且他们用于布局实在是无奈之举;

**flexbox在使用时,我们最担心的是它的兼容性问题:**

* 我们可以在 https://caniuse.com/ 上查询到具体的兼容性

# 二、flex布局的理解
**两个重要的概念:**

* 开启了 flex 布局的元素叫 flex container(容器)
* flex container 里面的直接子元素叫做 flex item

**当flex container中的子元素变成了flex item时,具备一下特点:**

* flex item的布局将受flex container属性的设置来进行控制和布局
* flex item<mark class="hltr-orange">不再严格区分块级元素和行内级元素</mark>;
	* 可以理解为<mark class="hltr-orange">行内块级元素</mark>
* flex item默认情况下是包裹内容的,但是可以设置宽度和高度

**设置 display 属性为 flex 或者inline-flex 可以成为 flex container**

* flex: flex container 以 block-level 形式存在
* inline-flex:flex container 以 inline-level 形式存在

> felx container 既可以是块级元素也可以是行内级元素。

# 三、flex布局模型
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723723438000tdawbl.png)

| 英文         | 中文  |
| ---------- | --- |
| main axis  | 主轴  |
| cross axis | 交叉轴 |

item 默认按照主轴排列

# 四、flex-container属性

**应用在 flex container 上的 CSS 属性**

* flex-flow（ditection 和 wrap 的简写属性）
* flex-direction（主轴方向）
* flex-wrap（单行还是多行显示）
* justify-content（决定 main axis 上 item 的分布方式）
* align-items（确定 item 在主轴上的对齐方式）
* align-content

## 4.1 flex-direction
direction-方向

**flex items 默认都是沿着 main axis(主轴)从 main start 开始往 main end 方向排布**

* flex-direction快定了 main axis的方向，有4个取值
* row(默认值)、row-reverse、column、column-reverse

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723725072000b3ar3b.png)


## 4.2 flex-wrap
wrap-包裹

**flex-wrap 决定了 flex container 是单行还是多行**

* nowrap(**默认**):单行
* wrap:多行
* wrap-reverse:多行(对比wrap，cross start与cross end 相反)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723725604000r82po7.png)

## 4.3 flex-flow
flow-流

**flex-flow 属性是 flex-direction 和flex-wrap 的简写。**

* 顺序任何,并且都可以省略;
* 语法结构`<'flex-direction'> || <'flex-wrap'>

## 4.4 justify-content
justigy-两端对齐

**justify-content 决定了flex items 在 main axis 上的对齐方式**

* flex-start(**默认值**):与main start 对齐
* flex-end:与main end 对齐
* center:居中对齐
* space-between（空间在两者之间）:
	* flex items 之间的距离相等
	* 与 main start、main end两端对齐
* space-around（空间环绕）:
	* flex items 之间的距离相等
	* flex items 与 main start、main end 之间的距离是 flex items 之间距离的一半
* space-evenly（空间均匀分布）:
	* flex items 之间的距离相等
	* flex items与 main start、main end 之间的距离 等于 fex items 之间的距离

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723727441000076snc.png)

> [!tip] 重点
> item 是 container 的内容，所以它对齐的是**内容的边框**，可以对 container 设置 boder、padding、margin的。

## 4.6 align-iems
**align-items决定了flex items 在 cross axis 上的对齐方式**

* normal:在**弹性布局**中，**效果和stretch一样**
* stretch:当flex items在cross axis 方向的 size 为 auto 时，会自动拉伸至填充 flex container
* flex-start:与 cross start 对齐
* flex-end:与cross end 对齐
* center:居中对齐
* baseline:与基准线对齐

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723874480000ix186p.png)

## 4.7 align-content
**align-content 决定了多行flex items 在 cross axis 上的对齐方式，用法与justify-content 类似**

* stretch(默认值):与 align-items 的stretch 类似
* flex-start:与cross start 对齐
* flex-end:与cross end 对齐
* center:居中对齐
* space-between:
	* flex items 之间的距离相等
	* 与 cross start、cross end两端对齐
*  space-around:
	* flex items 之间的距离相等
	* flex items与 cross start、cross end 之间的距离是 flex items 之间距离的一半
* space-evenly:
	* flex items 之间的距离相等
	* flex items与 cross start、cross end 之间的距离 等于 flex items 之间的距离

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723875509000mj3qfa.png)


# 五、flex-item属性

**应用在 flex items 上的 CSS 属性**

* flex-grow
* flex-basis
* flex-shrink
* order
* align-self
* flex

## 5.1 order
**order 决定了 flex items 的排布顺序**

* 在不改变 html 结构的同时进行排布
* 可以设置**任意整数**(正整数、负整数、0)，值越小就越排在前面
* 默认值是 0

## 5.2 align-self
**flex items 可以通过 align-self 覆盖 flex  container 设置的 align-items**

* auto(默认值):遵从fex container 的 align-items 设置
* stretch、flex-start、flex-end、center、 baseline,
* 效果跟 [[09 Flex布局#四、flex-container属性#4.6 align-iems|align-items]] 一致

## 5.3 flex-grow
**flex-grow 决定了 flex items 如何扩展(拉伸/成长)**

* 可以设置任意非负数字(正小数、正整数、0)，默认值是 0
* 当 flex container 在 main axis 方向上有**剩余size 时，flex-grow 属性才会有效**

**如果所有 flex items 的 flex-grow 总和 sum 超过 1，每个 fex item 扩展的 size 为**

 
 * flex container 的剩余 `size*flex-grow/sum`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723877167000lgtge4.png)

**flex items 扩展后的最终size 不能超过 `max-width、max-height`**


## 5.4 flex-shrink
**flex-shrink 决定了 fex items 如何收缩(缩小)**

* 可以设置任意非负数字(正小数、正整数、0)，**默认值是 1**
* 当 fex items 在 main axis 方向上超过了 flex container 的 size,flex-shrink 属性才会有效

**如果所有 flex items 的 fex-shrink 总和超过 1，每个 flex item 收缩的 size为**

* flex items 超出 fex container 的` size*收缩比例/所有 flex items 的收缩比例之和`

**flexitems 收缩后的最终size 不能小于` min-width、min-height`**

## 5.5 flex-basis
**flex-basis用来设置flex items 在 main axis 方向上的 base size**

* auto(默认值)
* 具体的宽度数值(100px)

**决定 fex items 最终 base size 的因素，从优先级高到低**

* `max-width\max-height\min-width\min-height`
* flex-basis
* width、height
* 内容本身的 size

## 5.6 flex(缩写属性)
 **flex是 flex-grow | flex-shrink | flex-basis 的简写,flex 属性可以指定1个，2个或3个值。**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723878631000f8pyhb.png)

前面的 none 就是`flex:none;`表示 `flex: 0 0 auto`

`|和||` 表示或者的意思 ，正确的应该还有一个 auto 的 `flex:auto;` 就表示的是 `felx: 1 1 auto`

而语法中的`?`就表示可以设置**一个或者零个**，当`flex:1;`的时候就默认是 `flex-shrink`是零个了。

**所以有下面的总结：**

**单值语法**: 值必须为以下其中之一:

* 一个无单位数(`<number>`):它会被当作`<flex-grow>`的值。
* 一个有效的宽度(width)值: 它会被当作 `<flex-basis>`的值。
* 关键字none，auto或initial.

> [!tip] 单值的特殊情况：
> 当前面设置过一个 `flex: 1;` 后在进行更改设置为 `flex; 0;` 这个时候的 0 并不是 `flex-grow` 而是 `flex-basis`。
> 解决办法是设置更改为 `flex: 0 auton` 这样就可以啦。
> 当然可以避免这样，就是进行 `flex` 缩写属性的编写的时候，把三个值都进行编写。

**双值语法**: 第一个值必须为一个无单位数，并且它会被当作`<flex-grow>`的值。

* 第二个值必须为以下之一:
	* 一个无单位数:它会被当作`<flex-shrink>`的值。
	* 一个有效的宽度值: 它会被当作`<flex-basis>`的值。

**三值语法:**

* 第一个值必须为一个无单位数，并且它会被当作`<flex-grow>`的值。
* 第二个值必须为一个无单位数，并且它会被当作`<fex-shrink>`的值。
* 第三个值必须为一个有效的宽度值，并且它会被当作`<flex-basis>`的值。

> [!tip] 重点
> flex 缩写属性具有一定的[[元素语义化及SEO#二、SEO|SEO]]，在使用过程中尽量使用缩写属性。

# 六、flex 常见问题

## 6.1 如下布局如何解决对齐问题

让最后一排也依次排列

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17238801540002gw19b.png)

可以通过直接计算，确定 `margin-right`，而不在`container`里面设置`justify-content: space-betweend;`

也可以通过在 container 的里面的 item 元素的后面**添加 row(列)-1个元素（i、span、div）都可以**，但是要对添加的元素设置和 **item 同样的宽度、高度为0**，这样就不会显示出来。

## 6.2 flex: 1; 的问题
先观察代码：

```html
<style>
	.contaner {
		display: flex;
		width: 110px;
		height: 100px;
	}
	.contaner .item {
		flex: 1;
		background-color: aquamarine;
	}
	.contaner .item .content {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
</style>

<div class="contaner">
	<div class="item">
		<div class="content">
			dfasfsafdsafdsafjdlkjffd
		</div>
	</div>
</div>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17257098020004othih.png)

对 content 进行了设置，但是不起作用，超出的内容还是会显示出来，并且把 包裹的盒子 item 撑了起来，**并且超过了包裹 item 的盒子 contaner 的宽度。**

这一切产生的原因是 item 盒子里面设置了 `flex: 1;`对应 flex-item 属性里面的 `flex-grow` 可以增长。

设置这个属性后，item 包含的**子元素里面的内容超出包裹 item 的元素 contaner 的盒子**也会把 contaner 撑起来。

**解决这种问题的办法是在 `flex:1;` 设置的元素里面设置一个属性 `overflow: hidden;` 就可以啦。**









