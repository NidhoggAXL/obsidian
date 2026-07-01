*  获取系统时间[[时间戳]]。
*  编写形式中问题。
	* time定义的格式``time_t time(time_t *timer)``
	* [[rand和srand|srand]]中使用时``srand(time(NULL))``  * NULL为空指针。*
* 代码：
```c
#include <time.h>
srand(time(指针));
```



