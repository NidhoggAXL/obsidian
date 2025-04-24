
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




