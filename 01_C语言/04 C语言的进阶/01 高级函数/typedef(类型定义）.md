```c
int maint(){
	typedef unsigned int u_int;// 对 unsigned int 类型定义为u_int
	unsigned int a = 10;
	u_int b = 20; //前面已经定义，这里可以之间引用
	return 0;
}
```