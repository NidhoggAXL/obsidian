# 一、插入F的案例

案例是当我点击按钮时会在中间插入一个f；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456578600001ja10d.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745657868000c9z9ys.png)


# 二、Vue源码对于key的判断

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745657884000l42exg.png)


# 三、没有key的操作（源码）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745657897000md5xq8.png)


# 四、没有key的过程如下
我们会发现上面的diff算法效率并不高：

* c和d来说它们事实上并不需要有任何的改动； 
* 但是因为我们的c被f所使用了，所有后续所有的内容都要一次进行改动，并且最后进行新增；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745657949000pzucgw.png)


# 五、有key执行操作(源码)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745657973000gn7b3m.png)

# 六、有key的diff算法如下（一）
第一步的操作是从头开始进行遍历、比较：

* a和b是一致的会继续进行比较； 
* c和f因为key不一致，所以就会break跳出循环；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745658002000xct0fx.png)

第二步的操作是从尾部开始进行遍历、比较：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745658012000ihacm1.png)

# 七、有key的diff算法如下（二）

第三步是如果旧节点遍历完毕，但是依然有新的节点，那么就新增节点：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745658030000cgzw0i.png)

第四步是如果新的节点遍历完毕，但是依然有旧的节点，那么就移除旧节点：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745658039000ex7hae.png)


# 八、有key的diff算法如下（三）

第五步是最特色的情况，中间还有很多未知的或者乱序的节点：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745658060000pv98k5.png)


所以我们可以发现，Vue在进行diff算法的时候，会尽量利用我们的key来进行优化操作： 

* 在没有key的时候我们的效率是非常低效的； 
* 在进行插入或者重置顺序的时候，保持相同的key可以让diff算法更加的高效；




