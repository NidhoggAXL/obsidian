* signed （有符号）
	* int 等同与 signed int
```c
int a = -10;
int a= 10;
// 其实在编写程序时 int 前面省略了 signed ，表示了 a 是有符号的数字，及可以表示整数（+），也可以表示负数(-)
```

* unsiged (无符号)
```c
unsigned int a = -10;
//在这里因为有 unsigned ，无符号，没有正负之分，所以这里 a 也是 10
```