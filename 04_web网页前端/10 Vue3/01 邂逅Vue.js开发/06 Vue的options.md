# 一、data属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745404320000sjwda8.png)

# 二、methods属性

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745405789000qvaet1.png)

# 三、问题一：不能使用箭头函数？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745405997000b1lmfq.png)

# 四、问题二：this到底指向什么？

事实上Vue的源码当中就是对methods中的所有函数进行了遍历，并且通过bind绑定了this：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745406016000t4gchk.png)

# 五、其他属性

当然，这里还可以定义很多其他的属性，我们会在后续进行讲解： 

* 比如props、computed、watch、emits、setup等等； 
* 也包括很多的生命周期函数；


