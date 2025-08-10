# 一、单一状态树

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747834877000546i0h.png)


# 二、组件获取状态

处理在 template 中使用插值语法获取状态，也可以在使用 [[01 computed计算属性使用|position API 的 computed]] ：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17478351740005sr5zx.png)

但是，如果我们有很多个状态都需要获取话，可以使用**mapState的辅助函数**：这个的放回值就是函数。

* mapState的方式一：对象类型； 
* mapState的方式二：数组类型； 
* 也可以使用<mark class="hltr-orange">展开运算符和来原有的computed</mark>混合在一起；
	* 展开运算后得到的就是每一个字符串匹配数据的 computed 的函数，例如上面 computed 中的 count 函数

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747835671000fbqkpb.png)

# 三、在setup中使用
在setup中如果我们单个获取装是非常简单的： 

* 通过useStore拿到store后去获取某个状态即可； 
* 但是如果我们需要使用 mapState 的功能呢？

## 3.1 自己封装hook

默认情况下，Vuex并没有提供非常方便的使用mapState的方式，这里我们进行了一个函数的封装：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837054000ld2ah6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837299000zr2qan.png)

> 主要 bind 绑定，为什么要使用 bind 来绑定 this 到 store 呢？这是因为在 setup 中是不可以使用 this 的，这个时候就需要我们改变 this ，这样就可以使用this。


解构出来的本质是一个函数，而这个函数是 computed 中的属性，会使用到的this

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837244000o6nnbm.png)

## 3.1 解构和toRef结合使用(推荐)

[[05 解构Destructuring}|解构]] 和 [[05 ref知识点补充|toRefs]] 联合使用

* toRefs 保证是响应式
* 解构中如果有和data重复的数据，则可以起别名

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747837427000yuj9sc.png)


