qsort-库函数-排序
quick-sort-快速排序
[[03 特殊指针类型 void]]
```C
函数的声明为：
void qsort(void* base,
	size_t num,
	size_t width,
	int(*cmp)(const void *e1,conse void *e2)
	);

boid qsort(目标数组的首元素地址，比较元素的长度，比较元素的宽度（每个元素的大小-单位是字节），比较元素的方法);
比较方法的定义，形参必须是const void* 的类型来接收。
返回值若大于0则升序排列，等于0不变，小于0降序排列

第一个参数:待排序数组的收元素地址
第二个参数:待排序数组的元素个数
第三个参数:待排序数组的每个元素的大小-单位是字节
第四个参数:是函数指针，比较两个元素的所用函数的地址-这个函数使用者自己实现
		函数指针的两个参数是:待比较的两个元素的地址
#include <stdio.h>
#include <stdlib.h>//qsort的头文件
#include <string.h>//strcmp的头文件
int cmp_int(const void* e1,const void* e2)
{
	//用void接收，所以不可以直接解引用
	//（int*)强制类型转换我int*型后就可以解引用了
	return *(int*)e1-*(int*)e2;
}

int cmp_stu_by_name(const void* e1,const void* e2)
{
	//(strucr stu*)e1 结构体指针
	//name 是字符串的比较
	//字符串比较不能直接用><=来比较，应该用strcmp函数
	#strcpy 
	return strcmp(((struct stu*)e1)->name-((struct stu*)e2)->name);
}

int main()
{
	int arr[5]={4,3,2,1,0};
	struct stu s[2]={{"ao",20},{"haha",30}};
	int len=sizeof(s)/sizeof(s[0]);
	int se=sizeof(arr)/sizeof(arr[0]);
	qsort(arr,se,sizeof(arr[0]),cmp_int)
	int i = 0;
	for ( i = 0 ; i < se ; i++ )
	{
		printf("%d ",arr[i]);
	}

	qsort(s,len,sizeof(s[0]),cmp_stu_by_name);
	
	return 0;
}

```


