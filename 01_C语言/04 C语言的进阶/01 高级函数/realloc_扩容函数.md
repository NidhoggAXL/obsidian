realloc的扩容分为两种-都要付出代价。
```
为了满足需要，我们每次扩容都是扩大两倍。这样比较合理
但是也可能会导致一定的空间浪费
```
1. 原地扩容-代价较小![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1705213099000dug0t9.png)

2. 异地扩容（开辟新空间，拷贝数据，在销毁原数据）![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17052131160005zwp6v.png)
