# static修饰局部变量
* 局部变量的生命周期变长
*  正常情况下[[局部变量和全局变量|局部变量]]
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1705213141000z9pitr.png)


* static修饰后的局部变量
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17052131540006xynxw.png)


# static修饰全局变量
* 改变了变量的作用域—让静态的[[局部变量和全局变量|全局变量]]只能在自己所在的源文件内部使用，出了源文件没法再使用了.
* static修饰函数该表了函数的链接属性（普通的一个函数具有**外部链接属性**可以使用[[extern(声明外部符号)]]在本源代码文件中使用），使用了static修饰函数后就变为了**内部链接属性**，只可以在本源代码文件中使用。
* 源文件说明![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1705213169000zrbbpx.png)


* 不能使用的情况![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1705213182000xknuze.png)
