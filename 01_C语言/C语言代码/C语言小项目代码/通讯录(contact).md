Contact
1. [[#contact.h 声明函数]]
2. [[#contact.c 实现函数的功能]]
3. [[#text.c 测试]]

> [!tip] 在不改变形参下，还是传地址的好处
> 这里使用到了结构体，如果是结构体过大，每次过来都要对结构体进行一次临时的拷贝。这样会大大的浪费空间，如果只是传地址的话，那指针接收拷贝的只是一个指针的大小，可以节省空间。

# 通讯录的功能
> 1. 存放1000个好友的信息
> 	1. 姓名
> 	2. 电话
> 	3. 性别
> 	4. 住址
> 	5. 年龄
> 2. 增加好友信息
> 3. 删除指定名字好友的信息
> 4. 查找好友的信息
> 5. 修改好友信息
> 6. 打印好友信息

# 静态版本通讯录
## 结构体的定义
使用结构体的嵌套来定义函数。
```C
#define MAX 1000
#define MAX_NAME 20
#define MAX_SEX 5
#define MAX_TELE 12
#define MAX_ADDR 30

struct PeoInfo
{
	char name[MAX_NAME];
	int age;
	char sex[MAX_SEX];
	char tele[MAX_TELE];
	char addr[MAX_ADDR];
};

struct Contact
{
	struct PeoInfo data[MAX];//存放一千个信息
	int size;//记录当前已经有的元素个数
};
```

## 菜单栏
```C
void menu()
{
	printf("****************************************\n");
	printf("*****1.add(增)         2. del(删)*******\n");
	printf("*****3.search(查)      4. modify(改)****\n");
	printf("*****5.show(显示)      6. sort(排序)****\n");
	printf("************0. exit(退出) **************\n");
	printf("****************************************\n");
}

int main()
{
	int input=0;
	struct Contact con;//con就是通讯录，里面包含：1000个元素和size
	InitContact(&con);
	do
	{
		menu();
		printf("请选择->");
		scanf("%d", &input);
		switch (input)
		{
		case ADD://增
			AddContact(&con);
			break;
		case DEL://删
			DelContact(&con);
			break;
		case SEARCH://查
			SearchContact(&con);
			break;
		case MODIFY://改
			ModifyContact(&con);
			break;
		case SHOW://显示
			ShowContact(&con);
			break;
		case SORT://排序
			printf("使用冒泡排序来实现");
			break;
		case 0:
			printf("退出通讯录\n");
			break;
		default:
			printf("输入错误，请重新输入！\n");
			break;
		}

	} while (input);
	return 0;
}
```
这里使用枚举使代码的可读性大大提高。
#枚举
```C
//枚举的使用，在case语句中更加具有可读性
enum Option
{
	EXIT,
	ADD,
	DEL,
	SEARCH,
	MODIFY,
	SHOW,
	SORT
};
```



## 通讯录功能声明
```C
//声明函数
void InitContact(struct Contact* ps);//结构体初始化
void AddContact(struct Contact* ps);//添加成员
void ShowContact(const struct Contact* ps);//打印const保证指针不会改变

//删除指定的联系人
void DelContact(struct Contact* ps);

//查找打印信息
void SearchContact(const struct Contact* ps);

//修改信息
void ModifyContact(struct Contact* ps);

```

## 通讯录函数的定义
### 通讯录初始化
```C
void InitContact(struct Contact* ps)
{
	assert(ps);
	memset(ps->data, 0, sizeof(ps->data));
	ps->size = 0;//设置通讯录初始0个元素
}
```

### 增
```c
//添加成员
void AddContact(struct Contact* ps)
{
	assert(ps);
	if (ps->size == MAX)
	{
		printf("通讯录成员已经，无法添加\n");
	}
	else
	{
		printf("请输入姓名->");
		scanf("%s", ps->data[ps->size].name);
		printf("请输入年龄->");
		scanf("%d", &(ps->data[ps->size].age));
		printf("请输入性别->");
		scanf("%s", ps->data[ps->size].sex);
		printf("请输入电话->");
		scanf("%s", ps->data[ps->size].tele);
		printf("请输入地址->");
		scanf("%s", ps->data[ps->size].addr);
		ps->size++;
		printf("添加成功\n");
	}
}
```

### 删
```C
//删除
void DelContact(struct Contact* ps)
{
	assert(ps);
	printf("请输入要删除的人的名字->");
	char name[MAX_NAME];
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos==-1)
	{
		printf("要删除的人不在\n");
	}
	else
	{
		//删除数据
		int j;
		for (j = pos; j < ps->size - 1; j++)
		{
			ps->data[j] = ps->data[j + 1];
		}
		ps->size--;
		printf("删除成功\n");
	}
}
```
FindByName函数的使用是查找名字的下标，这是一个**子函数**不需要把功能定义出来，所以这里就可以使用一个[[static]]函数来使用，定义一个局部变量。
```C
//static修饰局部变量
//这只是一个子功能，不需要用户看到
//所以static以后，局部变量就不需要声明
static int FindByName(const struct Contact* ps, char name[MAX_NAME])
{
	assert(ps);
	int i;
	for (i = 0; i < ps->size; i++)
	{
		if (0 == strcmp(ps->data[i].name, name))
		{
			return i;
		}
	}
	return -1;//找不到的情况
}
```

### 查
```C
//查找
void SearchContact(const struct Contact* ps)
{
	assert(ps);
	char name[MAX_NAME];
	printf("请输入要查到人的名字->");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要查找的人不在\n");
	}
	else
	{
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
			ps->data[pos].name,
			ps->data[pos].age,
			ps->data[pos].sex,
			ps->data[pos].tele,
			ps->data[pos].addr);

	}
}
```

### 改
```C
void ModifyContact(struct Contact* ps)
{
	assert(ps);
	char name[MAX_NAME];
	printf("请输入要修改人的名字->");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要修改人的信息不存在\n");
	}
	else
	{
		printf("请输入姓名->");
		scanf("%s", ps->data[pos].name);
		printf("请输入年龄->");
		scanf("%d", &(ps->data[pos].age));
		printf("请输入性别->");
		scanf("%s", ps->data[pos].sex);
		printf("请输入电话->");
		scanf("%s", ps->data[pos].tele);
		printf("请输入地址->");
		scanf("%s", ps->data[pos].addr);
		printf("修改成功\n");
	}
}
```

### 显示
```C
//打印，const保证指针不会改变
void ShowContact(const struct Contact* ps)
{
	assert(ps);
	if (ps->size == 0)
	{
		printf("通讯录为空\n");
	}
	else
	{
		int i = 0;
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		for (i = 0; i < ps->size; i++)
		{
			printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
				ps->data[i].name,
				ps->data[i].age,
				ps->data[i].sex,
				ps->data[i].tele,
				ps->data[i].addr );
		}
	}
}
```

### 排序
排序有多种排序，可以是名字、年龄……。
看使用什么排序的方法
[[01_C语言/算法 1/冒泡排序]]

### const的使用
const在这次代码中使用，是因为在传参过程中，希望传过来的形参不希望被改变

## contact.h 声明函数
```C
#pragma once
#include <stdio.h>
#include <assert.h>
#include <string.h>

#define MAX 1000
#define MAX_NAME 20
#define MAX_SEX 5
#define MAX_TELE 12
#define MAX_ADDR 30

struct PeoInfo
{
	char name[MAX_NAME];
	int age;
	char sex[MAX_SEX];
	char tele[MAX_TELE];
	char addr[MAX_ADDR];
};

//枚举的使用，在case语句中更加具有可读性
enum Option
{
	EXIT,
	ADD,
	DEL,
	SEARCH,
	MODIFY,
	SHOW,
	SORT
};

struct Contact
{
	struct PeoInfo data[MAX];//存放一千个信息
	int size;//记录当前已经有的元素个数
};

//声明函数
void InitContact(struct Contact* ps);//结构体初始化
void AddContact(struct Contact* ps);//添加成员
void ShowContact(const struct Contact* ps);//打印const保证指针不会改变

//删除指定的联系人
void DelContact(struct Contact* ps);

//查找打印信息
void SearchContact(const struct Contact* ps);

//修改信息
void ModifyContact(struct Contact* ps);

```

## contact.c 实现函数的功能
```C
#define _CRT_SECURE_NO_WARNINGS 1
#include "contact.h"

void InitContact(struct Contact* ps)
{
	assert(ps);
	memset(ps->data, 0, sizeof(ps->data));
	ps->size = 0;//设置通讯录初始0个元素
}

//添加成员
void AddContact(struct Contact* ps)
{
	assert(ps);
	if (ps->size == MAX)
	{
		printf("通讯录成员已经，无法添加\n");
	}
	else
	{
		printf("请输入姓名->");
		scanf("%s", ps->data[ps->size].name);
		printf("请输入年龄->");
		scanf("%d", &(ps->data[ps->size].age));
		printf("请输入性别->");
		scanf("%s", ps->data[ps->size].sex);
		printf("请输入电话->");
		scanf("%s", ps->data[ps->size].tele);
		printf("请输入地址->");
		scanf("%s", ps->data[ps->size].addr);
		ps->size++;
		printf("添加成功\n");
	}
}

//打印，const保证指针不会改变
void ShowContact(const struct Contact* ps)
{
	assert(ps);
	if (ps->size == 0)
	{
		printf("通讯录为空\n");
	}
	else
	{
		int i = 0;
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		for (i = 0; i < ps->size; i++)
		{
			printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
				ps->data[i].name,
				ps->data[i].age,
				ps->data[i].sex,
				ps->data[i].tele,
				ps->data[i].addr );
		}
	}
}

//static修饰局部变量
//这只是一个子功能，不需要用户看到
//所以static以后，局部变量就不需要声明
static int FindByName(const struct Contact* ps, char name[MAX_NAME])
{
	assert(ps);
	int i;
	for (i = 0; i < ps->size; i++)
	{
		if (0 == strcmp(ps->data[i].name, name))
		{
			return i;
		}
	}
	return -1;//找不到的情况
}

//删除
void DelContact(struct Contact* ps)
{
	assert(ps);
	printf("请输入要删除的人的名字->");
	char name[MAX_NAME];
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos==-1)
	{
		printf("要删除的人不在\n");
	}
	else
	{
		//删除数据
		int j;
		for (j = pos; j < ps->size - 1; j++)
		{
			ps->data[j] = ps->data[j + 1];
		}
		ps->size--;
		printf("删除成功\n");
	}
}

//查找
void SearchContact(const struct Contact* ps)
{
	assert(ps);
	char name[MAX_NAME];
	printf("请输入要查到人的名字->");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要查找的人不在\n");
	}
	else
	{
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
			ps->data[pos].name,
			ps->data[pos].age,
			ps->data[pos].sex,
			ps->data[pos].tele,
			ps->data[pos].addr);

	}
}

//修改信息
void ModifyContact(struct Contact* ps)
{
	assert(ps);
	char name[MAX_NAME];
	printf("请输入要修改人的名字->");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要修改人的信息不存在\n");
	}
	else
	{
		printf("请输入姓名->");
		scanf("%s", ps->data[pos].name);
		printf("请输入年龄->");
		scanf("%d", &(ps->data[pos].age));
		printf("请输入性别->");
		scanf("%s", ps->data[pos].sex);
		printf("请输入电话->");
		scanf("%s", ps->data[pos].tele);
		printf("请输入地址->");
		scanf("%s", ps->data[pos].addr);
		printf("修改成功\n");
	}
}
```
## text.c 测试
```C
#define _CRT_SECURE_NO_WARNINGS 1
#include "contact.h"
void menu()
{
	printf("****************************************\n");
	printf("*****1.add(增)         2. del(删)*******\n");
	printf("*****3.search(查)      4. modify(改)****\n");
	printf("*****5.show(显示)      6. sort(排序)****\n");
	printf("************0. exit(退出) **************\n");
	printf("****************************************\n");
}

int main()
{
	int input=0;
	struct Contact con;//con就是通讯录，里面包含：1000个元素和size
	InitContact(&con);
	do
	{
		menu();
		printf("请选择->");
		scanf("%d", &input);
		switch (input)
		{
		case ADD://增
			AddContact(&con);
			break;
		case DEL://删
			DelContact(&con);
			break;
		case SEARCH://查
			SearchContact(&con);
			break;
		case MODIFY://改
			ModifyContact(&con);
			break;
		case SHOW://显示
			ShowContact(&con);
			break;
		case SORT://排序
			printf("使用冒泡排序来实现");
			break;
		case 0:
			printf("退出通讯录\n");
			break;
		default:
			printf("输入错误，请重新输入！\n");
			break;
		}

	} while (input);
	return 0;
}
```
# 动态版本通讯录
> 默认可以存放3个人的信息
> 当发现当前通讯录满的时候，进行扩容，每次增加2个空间
>  优点：
> 对空间的利用率更高

> [!tip] 注意动态内存的问题：
> 只有增加的时候会涉及到容量的变化，需要进行增容。
## Contact.h
```C
#pragma once
#include <stdio.h>
#include <assert.h>
#include <string.h>
#include <stdlib.h>//开辟空间
#include <errno.h>//打印错误

//#define MAX 1000
#define MAX_NAME 20
#define MAX_SEX 5
#define MAX_TELE 12
#define MAX_ADDR 30
#define CAPACITY 3//初始容量

//枚举的使用，在case语句中更加具有可读性
enum Option
{
	EXIT,
	ADD,
	DEL,
	SEARCH,
	MODIFY,
	SHOW,
	SORT
};

struct PeoInfo
{
	char name[MAX_NAME];
	int age;
	char sex[MAX_SEX];
	char tele[MAX_TELE];
	char addr[MAX_ADDR];
};

struct Contact
{
	struct PeoInfo* data;
	int size;//记录当前已经有的元素个数
	int capacity;//当前通讯录的最大容量
};

//声明函数
void InitContact(struct Contact* ps);//结构体初始化
void AddContact(struct Contact* ps);//添加成员
void ShowContact(const struct Contact* ps);//打印const保证指针不会改变

//删除指定的联系人
void DelContact(struct Contact* ps);

//查找打印信息
void SearchContact(const struct Contact* ps);

//修改信息
void ModifyContact(struct Contact* ps);

//释放内存
void DestoryContact(struct Contact* ps);
```
## text.c
```C
#define _CRT_SECURE_NO_WARNINGS 1
#include "contact.h"
void menu()
{
	printf("****************************************\n");
	printf("*****1.add(增)         2. del(删)*******\n");
	printf("*****3.search(查)      4. modify(改)****\n");
	printf("*****5.show(显示)      6. sort(排序)****\n");
	printf("************0. exit(退出) **************\n");
	printf("****************************************\n");
}

int main()
{
	int input=0;
	struct Contact con;//con就是通讯录，里面包含：dada指针和size、capaticy
	//初始化通讯录
	InitContact(&con);
	do
	{
		menu();
		printf("请选择->");
		scanf("%d", &input);
		switch (input)
		{
		case ADD://增
			AddContact(&con);
			break;
		case DEL://删
			DelContact(&con);
			break;
		case SEARCH://查
			SearchContact(&con);
			break;
		case MODIFY://改
			ModifyContact(&con);
			break;
		case SHOW://显示
			ShowContact(&con);
			break;
		case SORT://排序
			printf("使用冒泡排序来实现");
			break;
		case 0:
			//销毁通讯录，释放动态开辟的内存
			DestoryContact(&con);
			printf("退出通讯录\n");
			break;
		default:
			printf("输入错误，请重新输入！\n");
			break;
		}

	} while (input);
	return 0;
}
```

## Contact.c
```C
#define _CRT_SECURE_NO_WARNINGS 1
#include "contact.h"

void InitContact(struct Contact* ps)
{
	assert(ps);
	//开辟三个空间
	ps->data = (struct PeoInfo*)malloc(CAPACITY * sizeof(struct PeoInfo));
	if (ps->data==NULL)
	{
		printf("%s\n", strerror(errno));
	}
	ps->capacity = CAPACITY;
	ps->size = 0;//设置通讯录初始0个元素
}

//检查容量
//static修饰局部变量
//这只是一个子功能，不需要用户看到
//所以static以后，局部变量就不需要声明
static void CheckCapacity(struct Contact* ps)
{
	assert(ps);
	if (ps->size == ps->capacity)
	{
		printf("容量不够，进行增容\n");
		struct PeoInfo* ptr = realloc(ps->data, (ps->capacity + 2) * sizeof(struct PeoInfo));
		if (ptr != NULL)
		{
			printf("增容成功\n");
			ps->data = ptr;
			ps->capacity += 2;
		}
		else
		{
			printf("增容失败\n");
			return 0;
		}
	}
 }//这里可以看出，改变内存容量的时候，不需要考虑形参和实参的关系

//添加成员
void AddContact(struct Contact* ps)
{
	assert(ps);
	CheckCapacity(ps);//检查容量
	//添加成员
	printf("请输入姓名->");
	scanf("%s", ps->data[ps->size].name);
	printf("请输入年龄->");
	scanf("%d", &(ps->data[ps->size].age));
	printf("请输入性别->");
	scanf("%s", ps->data[ps->size].sex);
	printf("请输入电话->");
	scanf("%s", ps->data[ps->size].tele);
	printf("请输入地址->");
	scanf("%s", ps->data[ps->size].addr);
	ps->size++;
	printf("添加成功\n");
}

//打印，const保证指针不会改变
void ShowContact(const struct Contact* ps)
{
	assert(ps);
	if (ps->size == 0)
	{
		printf("通讯录为空\n");
	}
	else
	{
		int i = 0;
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		for (i = 0; i < ps->size; i++)
		{
			printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
				ps->data[i].name,
				ps->data[i].age,
				ps->data[i].sex,
				ps->data[i].tele,
				ps->data[i].addr );
		}
	}
}

//static修饰局部变量
//这只是一个子功能，不需要用户看到
//所以static以后，局部变量就不需要声明
static int FindByName(const struct Contact* ps, char name[MAX_NAME])
{
	assert(ps);
	int i;
	for (i = 0; i < ps->size; i++)
	{
		if (0 == strcmp(ps->data[i].name, name))
		{
			return i;
		}
	}
	return -1;//找不到的情况
}

//删除
void DelContact(struct Contact* ps)
{
	int pos;
	assert(ps);
	printf("请输入要删除的人的名字->");
	char name[MAX_NAME];
	scanf("%s", name);
	pos = FindByName(ps, name);
	if (pos==-1)
	{
		printf("要删除的人不在\n");
	}
	else
	{
		//删除数据
		int j;
		for (j = pos; j < ps->size - 1; j++)
		{
			ps->data[j] = ps->data[j + 1];
		}
		ps->size--;
		printf("删除成功\n");
	}
}

//查找
void SearchContact(const struct Contact* ps)
{
	int pos;
	assert(ps);
	char name[MAX_NAME];
	printf("请输入要查到人的名字->");
	scanf("%s", name);
	pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要查找的人不在\n");
	}
	else
	{
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
			ps->data[pos].name,
			ps->data[pos].age,
			ps->data[pos].sex,
			ps->data[pos].tele,
			ps->data[pos].addr);

	}
}

//修改信息
void ModifyContact(struct Contact* ps)
{
	assert(ps);
	int pos;	
	char name[MAX_NAME];
	printf("请输入要修改人的名字->");
	scanf("%s", name);
	pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要修改人的信息不存在\n");
	}
	else
	{
		printf("请输入姓名->");
		scanf("%s", ps->data[pos].name);
		printf("请输入年龄->");
		scanf("%d", &(ps->data[pos].age));
		printf("请输入性别->");
		scanf("%s", ps->data[pos].sex);
		printf("请输入电话->");
		scanf("%s", ps->data[pos].tele);
		printf("请输入地址->");
		scanf("%s", ps->data[pos].addr);
		printf("修改成功\n");
	}
}


//释放内存
void DestoryContact(struct Contact* ps)
{
	assert(ps);
	free(ps->data);
	ps->data = NULL;
	//这里的ps-con不需要释放，因为con是我们定义出来的一块
	//空间，是一个局部变量，不是动态开辟出来的。
}
```



# 动态文件版通讯录
![[文件操作#文件的打开和关闭]]

[[文件操作#设备输入和输入-单行#fread和fwrite(二进制输入输出)]]

## Contact.c
```C
#define _CRT_SECURE_NO_WARNINGS 1
#include "contact.h"

//初始化
void InitContact(struct Contact* ps)
{
	assert(ps);
	//开辟三个空间
	ps->data = (struct PeoInfo*)malloc(CAPACITY * sizeof(struct PeoInfo));
	if (ps->data==NULL)
	{
		printf("InitContact:%s\n", strerror(errno));
	}
	ps->capacity = CAPACITY;
	ps->size = 0;//设置通讯录初始0个元素
	//把文件中已经存在的信息加载到通讯录中
	LoadContact(ps); 
}

//CheckCapacity在后面定义的，下面这个函数要使用就要声明一下
static void CheckCapacity(struct Contact* ps);
//加载文件中的信息到通讯录
void LoadContact(struct Contact* ps)
{
	struct PeoInfo tmp = { 0 };
	FILE* pfRead = fopen("contact.dat", "rb");
	if (pfRead == NULL)
	{
		printf("LoadContact:%s\n", strerror(errno));
		return;
	}
	//读取文件到通讯录中
	while (fread(&tmp, sizeof(struct PeoInfo), 1, pfRead))//读取的数据先存放到tmp中
	{	//fread 的放回值作为while的判断语句，一直读取，知道没有读取的时候放回0
		CheckCapacity(ps);//检查容量
		ps->data[ps->size] = tmp;
		ps->size++;
	}
	//关闭文件
	fclose(pfRead);
	pfRead = NULL;
}


//检查容量
//static修饰局部变量
//这只是一个子功能，不需要用户看到
//所以static以后，局部变量就不需要声明
static void CheckCapacity(struct Contact* ps)
{
	assert(ps);
	if (ps->size == ps->capacity)
	{
		printf("容量不够，进行增容\n");
		struct PeoInfo* ptr = realloc(ps->data, (ps->capacity + 2) * sizeof(struct PeoInfo));
		if (ptr != NULL)
		{
			printf("增容成功\n");
			ps->data = ptr;
			ps->capacity += 2;
		}
		else
		{
			printf("增容失败\n");
			return 0;
		}
	}
}//这里可以看出，改变内存容量的时候，不需要考虑形参和实参的关系

//添加成员
void AddContact(struct Contact* ps)
{
	assert(ps);
	CheckCapacity(ps);//检查容量
	//添加成员
	printf("请输入姓名->");
	scanf("%s", ps->data[ps->size].name);
	printf("请输入年龄->");
	scanf("%d", &(ps->data[ps->size].age));
	printf("请输入性别->");
	scanf("%s", ps->data[ps->size].sex);
	printf("请输入电话->");
	scanf("%s", ps->data[ps->size].tele);
	printf("请输入地址->");
	scanf("%s", ps->data[ps->size].addr);
	ps->size++;
	printf("添加成功\n");
}

//打印，const保证指针不会改变
void ShowContact(const struct Contact* ps)
{
	assert(ps);
	if (ps->size == 0)
	{
		printf("通讯录为空\n");
	}
	else
	{
		int i = 0;
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		for (i = 0; i < ps->size; i++)
		{
			printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
				ps->data[i].name,
				ps->data[i].age,
				ps->data[i].sex,
				ps->data[i].tele,
				ps->data[i].addr );
		}
	}
}

//static修饰局部变量
//这只是一个子功能，不需要用户看到
//所以static以后，局部变量就不需要声明
static int FindByName(const struct Contact* ps, char name[MAX_NAME])
{
	assert(ps);
	int i;
	for (i = 0; i < ps->size; i++)
	{
		if (0 == strcmp(ps->data[i].name, name))
		{
			return i;
		}
	}
	return -1;//找不到的情况
}

//删除
void DelContact(struct Contact* ps)
{
	int pos;
	assert(ps);
	printf("请输入要删除的人的名字->");
	char name[MAX_NAME];
	scanf("%s", name);
	pos = FindByName(ps, name);
	if (pos==-1)
	{
		printf("要删除的人不在\n");
	}
	else
	{
		//删除数据
		int j;
		for (j = pos; j < ps->size - 1; j++)
		{
			ps->data[j] = ps->data[j + 1];
		}
		ps->size--;
		printf("删除成功\n");
	}
}

//查找
void SearchContact(const struct Contact* ps)
{
	int pos;
	assert(ps);
	char name[MAX_NAME];
	printf("请输入要查到人的名字->");
	scanf("%s", name);
	pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要查找的人不在\n");
	}
	else
	{
		//标题
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-20s\n",
			"名字", "年龄", "性别", "电话", "地址");
		//数据
		printf("%-20s\t%-4d\t%-5s\t%-12s\t%-20s\n",
			ps->data[pos].name,
			ps->data[pos].age,
			ps->data[pos].sex,
			ps->data[pos].tele,
			ps->data[pos].addr);

	}
}

//修改信息
void ModifyContact(struct Contact* ps)
{
	assert(ps);
	int pos;	
	char name[MAX_NAME];
	printf("请输入要修改人的名字->");
	scanf("%s", name);
	pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要修改人的信息不存在\n");
	}
	else
	{
		printf("请输入姓名->");
		scanf("%s", ps->data[pos].name);
		printf("请输入年龄->");
		scanf("%d", &(ps->data[pos].age));
		printf("请输入性别->");
		scanf("%s", ps->data[pos].sex);
		printf("请输入电话->");
		scanf("%s", ps->data[pos].tele);
		printf("请输入地址->");
		scanf("%s", ps->data[pos].addr);
		printf("修改成功\n");
	}
}


//保存文件
void SaveContact(struct Contact* ps)
{
	assert(ps);
	int i;
	FILE* PfWrite = fopen("Contact.dat", "wb");
	if (PfWrite == NULL)
	{
		printf("SaveContact:%s\n", strerror(errno));
		return ;//void 没有返回值
	}
	//写通讯录的数据到文件
	for (i = 0; i < ps->size; i++)
	{ 
		fwrite(&(ps->data[i]), sizeof(struct PeoInfo), 1, PfWrite);
	}
	//关闭文件
	fclose(PfWrite); 
	PfWrite == NULL;
	printf("保存成功\n");
}

//释放内存
void DestoryContact(struct Contact* ps)
{
	assert(ps);
	free(ps->data);
	ps->data = NULL;
	//这里的ps-con不需要释放，因为con是我们定义出来的一块
	//空间，是一个局部变量，不是动态开辟出来的。
}
```

## text.c
```C
#define _CRT_SECURE_NO_WARNINGS 1
#include "contact.h"
void menu()
{
	printf("****************************************\n");
	printf("*****1.add(增)         2. del(删)*******\n");
	printf("*****3.search(查)      4. modify(改)****\n");
	printf("*****5.show(显示)      6. sort(排序)****\n");
	printf("*****7.save(存储)      0. exit(退出)****\n");
	printf("****************************************\n");
}

int main()
{
	int input=0;
	struct Contact con;//con就是通讯录，里面包含：dada指针和size、capaticy
	//初始化通讯录
	InitContact(&con);
	do
	{
		menu();
		printf("请选择->");
		scanf("%d", &input);
		switch (input)
		{
		case ADD://增
			AddContact(&con);
			break;
		case DEL://删
			DelContact(&con);
			break;
		case SEARCH://查
			SearchContact(&con);
			break;
		case MODIFY://改
			ModifyContact(&con);
			break;
		case SHOW://显示
			ShowContact(&con);
			break;
		case SORT://排序
			printf("使用冒泡排序来实现");
			break;
		case SAVE://保存到文件
			SaveContact(&con);
			break;
		case 0:
			SaveContact(&con);//如果忘记保存，在退出的时候自动保存一下
			//销毁通讯录，释放动态开辟的内存
			DestoryContact(&con);
			printf("退出通讯录\n");
			break;
		default:
			printf("输入错误，请重新输入！\n");
			break;
		}

	} while (input);
	return 0;
}
```

## Contact.c
```C
#pragma once
#include <stdio.h>
#include <assert.h>
#include <string.h>
#include <stdlib.h>//开辟空间
#include <errno.h>//打印错误

//#define MAX 1000
#define MAX_NAME 20
#define MAX_SEX 5
#define MAX_TELE 12
#define MAX_ADDR 30
#define CAPACITY 3//初始容量

//枚举的使用，在case语句中更加具有可读性
enum Option
{
	EXIT,
	ADD,
	DEL,
	SEARCH,
	MODIFY,
	SHOW,
	SORT,
	SAVE
};

struct PeoInfo
{
	char name[MAX_NAME];
	int age;
	char sex[MAX_SEX];
	char tele[MAX_TELE];
	char addr[MAX_ADDR];
};

struct Contact
{
	struct PeoInfo* data;
	int size;//记录当前已经有的元素个数
	int capacity;//当前通讯录的最大容量
};

//声明函数
void InitContact(struct Contact* ps);//结构体初始化
void AddContact(struct Contact* ps);//添加成员
void ShowContact(const struct Contact* ps);//打印const保证指针不会改变

//删除指定的联系人
void DelContact(struct Contact* ps);

//查找打印信息
void SearchContact(const struct Contact* ps);

//修改信息
void ModifyContact(struct Contact* ps);

//释放内存
void DestoryContact(struct Contact* ps);

//保存文件
void SaveContact(struct Contact* ps);

//加载文件中的信息到通讯录
void LoadContact(struct Contact* ps);
```