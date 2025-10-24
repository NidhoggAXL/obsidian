# 一、复杂data的处理方法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745659129000hd0ol7.png)


# 二、认识计算属性computed

什么是计算属性呢？ 

* 官方并没有给出直接的概念解释； 
* 而是说：对于<mark class="hltr-orange">任何包含响应式数据的复杂逻辑</mark>，你都应该使用计算属性；
* **计算属性**将被混入到组件实例中
	* 所有 getter 和 setter 的 this 上下文自动地绑定为组件实例； 

计算属性的用法：

* 选项：computed 
* 类型：`{ [key: string]: Function | { get: Function, set: Function } }`

# 三、案例实现思路

我们来看三个案例： 

**案例一**：我们有两个变量：firstName和lastName，希望它们拼接之后在界面上显示； 

**案例二**：我们有一个分数：score 

* 当score大于60的时候，在界面上显示及格； 
* 当score小于60的时候，在界面上显示不及格； 

**案例三**：我们有一个变量message，记录一段文字：比如Hello World 

* 某些情况下我们是直接显示这段文字； 
* 某些情况下我们需要对这段文字进行**反转**；
* 反转的思路是
	* 字符串->数组（[[05 数组Array#^ffadfe|splice]]）
	* 数组进行反转（[[05 数组Array#七、数组的排序|reverse]]）
	* 数组->字符串（[[05 数组Array#五、数组的方法-slice、concat、join|join]]）


**可以有三种实现思路：** 

* 思路一：在模板语法中直接使用表达式； 
* 思路二：使用method对逻辑进行抽取； 
* 思路三：使用计算属性computed；

# 四、实现思路一：模板语法

思路一的实现：模板语法 

* **缺点一**：模板中存在大量的复杂逻辑，不便于维护（<mark class="hltr-orange">模板中表达式的初衷是用于简单的计算</mark>）； 
* **缺点二**：当有多次一样的逻辑时，存在重复的代码； 
* **缺点三**：多次使用的时候，很多运算也需要多次执行，没有缓存；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745660133000h8z4qv.png)

# 五、实现思路二：method实现

思路二的实现：method实现 

* **缺点一**：我们事实上先显示的是一个结果，但是都变成了一种方法的调用； 
* **缺点二**：多次使用方法的时候，<mark class="hltr-orange">没有缓存</mark>，也需要多次计算；


![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1745660375000x0ktm3.png)

# 六、思路三的实现：computed实现

思路三的实现：computed实现 

* 注意：计算属性看起来像是一个函数，但是我们在使用的时候不需要加()，后面的[[03 computed的set和get|setter和getter]]有说明
* 我们会发现无论是直观上，还是效果上计算属性都是更好的选择； 
* 并且计算属性是<mark class="hltr-orange">有缓存</mark>的；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17456605330004e9hpg.png)



