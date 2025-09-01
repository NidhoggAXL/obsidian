内联样式是官方推荐的一种css样式的写法： 

- style 接受一个**采用小驼峰命名**属性的 JavaScript **对象**，，而不是 CSS 字符串； 
- 并且可以引用state中的状态来设置相关的样式； 

内联样式的优点: 

- 内联样式, 样式之间不会有冲突 
- 可以动态获取当前state中的状态 

内联样式的缺点： 

- 写法上都需要使用驼峰标识 
- 某些样式没有提示 
- 大量的样式, 代码混乱 
- 某些样式无法编写(比如[[09 伪类选择器|伪类]]/[[10 伪元素（pseudo-elements）|伪元素]]) 

所以官方依然是希望内联合适和普通的css来结合编写；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175532918800091thvl.png)

