* 代码使用格式
```c
#include <stdio.h>
memset(存储字符串的数组,'设计内容(不可以是字符串)',设计的个数-从开头开始（过多也会溢出）);
```

* 例子
```c
#include <stdio.h>
int main()
{
	char arr[]="hello world";
	memset(arr,'*',5);
	printf("%s\n",arr);
	return 0;
}
```

![[Pasted image 20230614123043.png]]
