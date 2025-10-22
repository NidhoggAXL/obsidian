# 一、绑定 class 介绍
在开发中，有时候我们的元素class也是动态的，比如

* 当数据为<mark class="hltr-orange">某个状态</mark>时，字体显示红色。
* 当数据<mark class="hltr-orange">另一个状态</mark>时，字体显示黑色,

绑定class有两种方式:

* 对象语法
* 数组语法

# 二、绑定class – 对象语法

**对象语法**：我们可以传给` :class (v-bind:class 的简写) `一个对象，以动态地切换 class。

```html
<button :class="{key: value}>内容</button>
```

* value **必须** 是一个**布尔类型**
* 如果 value 为真 true ，则为 button 添加 key 到 classlist 里面
* 如果为假，则反之

下面代码的需求是当点击按钮的时候，字体会变成红色：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745503871000495fps.png)

当点击变为红色字体时候，class 的状态：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745504139000n2c4sn.png)

# 三、绑定class – 数组语法(了解)

**数组语法**：我们可以把一个数组传给 `:class`，以应用一个 class 列表；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745504229000zmt0ti.png)


# 四、绑定style介绍
我们可以利用**v-bind:style**来绑定一些**CSS内联样式**

* 这次因为某些样式我们需要根据<mark class="hltr-orange">数据</mark>动态来决定;
* 比如某段文字的颜色，大小等等;

CSS property 名可以用<mark class="hltr-orange">驼峰式(camelCase)</mark>或<mark class="hltr-orange">短横线分隔(kebab-case，:记得用引号括起来</mark>)来命名;

绑定class有两种方式:

* 对象语法
* 数组语法
# 五、绑定style-对象语法

对象语法：

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745582800000vnxfxt.png)

# 六、板顶style-数组语法

**数组语法：**

* `:style` 的数组语法可以将<mark class="hltr-orange">多个样式对象</mark>应用到同一个元素上；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745582831000qicypx.png)
# 七、动态绑定属性(了解)


在某些情况下，我们属性的名称可能也不是固定的

* 前端无论绑定`｀src、href、class、style｀`，属性名称都是固定的
* 如果属性名称不是固定的，我们可以使用 `:[属性名]="值"` 的格式来定义； 
* 这种绑定的方式，我们称之为动态绑定属性

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745583678000yxhuwy.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745583692000p9032v.png)

# 八、绑定一个对象(重要)

如果我们希望将一个**对象的所有属性**，绑定**到元素上的所有属性**，应该怎么做呢？ 

* 非常简单，我们可以直接使用 **v-bind 绑定一个 对象；**

案例：info对象会被拆解成div的各个属性


![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17455839190000msb2l.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745583931000h9tl4e.png)


