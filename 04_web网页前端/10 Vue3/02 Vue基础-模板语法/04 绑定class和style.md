
# 一、绑定 class 介绍


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745502607000u9tzy3.png)

# 二、绑定class – 对象语法

**对象语法**：我们可以传给` :class (v-bind:class 的简写) `一个对象，以动态地切换 class。

```
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


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745582265000z7lha6.png)


# 五、绑定style-对象、数组语法

对象语法：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745582800000vnxfxt.png)

数组语法：

* `:style` 的数组语法可以将多个样式对象应用到同一个元素上；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745582831000qicypx.png)


# 六、动态绑定属性(了解)


在某些情况下，我们属性的名称可能也不是固定的

* 前端我们无论绑定`｀src、href、class、style｀`，属性名称都是固定的
* 如果属性名称不是固定的，我们可以使用 `:[属性名]="值"` 的格式来定义； 
* 这种绑定的方式，我们称之为动态绑定属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745583678000yxhuwy.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745583692000p9032v.png)

# 七、绑定一个对象(重要)

如果我们希望将一个**对象的所有属性**，绑定**到元素上的所有属性**，应该怎么做呢？ 

*　非常简单，我们可以直接使用 **v-bind 绑定一个 对象；**

案例：info对象会被拆解成div的各个属性


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17455839190000msb2l.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745583931000h9tl4e.png)


