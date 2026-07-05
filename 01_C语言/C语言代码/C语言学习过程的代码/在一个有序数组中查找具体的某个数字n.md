```c
//在一个有序数组中查找具体的某个数字n。
#include <stdio.h>
int main()
{
	int arr[]={1,2,3,4,5,6,7,8,9,10};
	int m = 0;
	int i = 0;
	scanf("%d",&m);
	int se = sizeof(arr)/sizeof(arr[0]);
	for (i = 0;i<se;i++)
	{
		if (m == arr[i])
		{
			printf("找到了，下标是；%d\n",i);
			break ;
		}
	}
	if (m == se)
	{
		printf("找不到\n"); 
	}
	return 0;
}
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1705215115000auzgfw.png)


* 改进
![[（有序大小）折半 二分查找算法]]
