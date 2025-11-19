在React开发中，我们总是会强调数据的不可变性： 

- 无论是类组件中的state，还是redux中管理的state； 
- 事实上在整个JavaScript编码过程中，数据的不可变性都是非常重要的； 

所以在前经常会进行浅拷贝来完成某些操作，但是浅拷贝事实上也是存在问题的： 

- 比如过大的对象，进行浅拷贝也会造成性能的浪费； 
- 比如浅拷贝后的对象，在深层改变时，依然会对之前的对象产生影响； 

事实上Redux Toolkit底层使用了immer.js的一个库来保证数据的不可变性。 

在公众号的一片文章中也有专门讲解immutable-js库的底层原理和使用方法： 

- https://mp.weixin.qq.com/s/hfeCDCcodBCGS5GpedxCGg 

为了节约内存，又出现了一个新的算法：Persistent Data Structure（持久化数据结构或一致性 数据结构）；

- 用一种数据结构来保存数据； 
- 当数据被修改时，会返回一个对象，但是新的对象会尽可能的利用之前的数据结构而不会 对内存造成浪费；

![](https://mmbiz.qpic.cn/mmbiz_gif/O8xWXzAqXuuPtxc2VNSb80zpYnIGMuvn6vRJMGliaqLp8wWNEgKOVutM4vjiaiaGD0iba6tYMQ8DFV8MsYzC7via0bg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

