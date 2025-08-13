# 一、React列表渲染

真实开发中我们会从服务器请求到大量的数据，数据会以列表的形式存储： 

- 比如歌曲、歌手、排行榜列表的数据； 
- 比如商品、购物车、评论列表的数据； 
- 比如好友消息、动态、联系人列表的数据；

在React中并**没有像Vue模块语法中的v-for指令**，而且需要我们通过JavaScript代码的方式组织数据，转成JSX： 

- 很多从Vue转型到React的同学非常不习惯，认为Vue的方式更加的简洁明了； 
- 但是React中的JSX正是因为和JavaScript无缝的衔接，让它可以更加的灵活； 
- 另外我经常会提到**React是真正可以提高我们编写代码能力的一种方式**；

如何展示列表呢？ 

- 在React中，展示列表最多的方式就是使用数组的[[09 数据结构-Map映射|map高阶函数]]；

很多时候我们在展示一个数组中的数据之前，需要先对它进行一些处理：

- 比如过滤掉一些内容：[[05 数组Array#8.1 filter-过滤|filter函数]] 
- 比如截取数组中的一部分内容：[[05 数组Array#五、数组的方法-slice、concat、join|slice函数]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754998510000nxhvjt.png)


# 二、列表中的key

我们会发现在前面的代码中只要展示列表都会报一个警告：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754998553000bd5sq5.png)

个警告是告诉我们需要在列表展示的jsx中添加一个key。 

- key主要的作用是为了提高diff算法时的效率；
- 这个我们在后续内容中再进行讲解；


