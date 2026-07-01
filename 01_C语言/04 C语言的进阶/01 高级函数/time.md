*  获取系统时间[[01_C语言/01 C语言基础/时间戳]]。
*  编写形式中问题。
	* time定义的格式``time_t time(time_t *timer)``
	* [[01_C语言/04 C语言的进阶/01 高级函数/rand和srand|srand]]中使用时``srand(time(NULL))``  * NULL为空指针。*
* 代码：
```c
#include <time.h>
srand(time(指针));
```



