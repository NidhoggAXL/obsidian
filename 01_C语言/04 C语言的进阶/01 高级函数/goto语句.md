*  goto语句的运用场景：C语言中提供了可以**随意滥用**的goto语句和标记跳转的标号**从理论上 goto语句是没有必要的**，实践中没有goto语句也可以很容易的写出代码但是某些场合下goto语句还是用得着的，最**常见的用法就是终止程序在某些深度嵌套的结构的处理过程**，会打乱C语言代码执行的结构（随意乱跳）。例如一次跳出两层或多层循环。这种情况使用break是达不到目的的。它只能从最内层循环退出到上一层的循环。
*  goto语句的格式
```c
int main()
{
	printf("haha\n");
(定义格式语句)
	printf("你好\n");
	goto (定义格式语句)；
	printf("hehe\n")；
	retuen 0;
}
```

* goto语言真正适合的场景如下：
	* 跳出生层次的嵌套结构![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1705212826000y9miok.png)
		*  ![[关机代码|字符串关机代码]]


*  代码：
	1. 死循环的运用。
```c
#include <stdio.h>
int main()
{
	printf("haha\n");
agan:
	printf("你好\n");
	goto agan;
	printf("hehe\n");
	return 0;
}
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17052130690000afs5f.png)


