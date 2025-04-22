```C
int a = 10;
int *p= &a;
void *p= &a;

char ch='w';
void *p = &ch;
p=&a;

void 类型的指针可以接受任何类型的地址
```

> [!tip] 需要注意的
> void指针不能进行解引用操作和+-整数的操作
> ```
> int main()
> {
> 	int a= 10;
> 	void* p =&a;
> 	*p = 20;//错误
> }
> ```


