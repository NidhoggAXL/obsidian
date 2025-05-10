# 一、认识keep-alive
我们先对之前的案例中About组件进行改造： 

在其中增加了一个按钮，点击可以递增的功能；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746866996000ghn145.png)

比如我们将counter点到10，那么在切换到home再切换回来about时，状态是否可以保持呢？ 

* 答案是否定的； 
* 这是因为默认情况下，我们在**切换组件后，about组件会被销毁掉，再次回来时会重新创建组件；**

但是，在开发中某些情况我们希望<mark class="hltr-orange">继续保持组件的状态，而不是销毁掉</mark>，这个时候我们就可以使用一个内置组件：keep-alive。


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17468670530009t9f8u.png)


# 二、keep-alive属性
keep-alive有一些属性： 

* include - `string | RegExp | Array`。只有名称匹配的组件会被缓存； 
* exclude - `string | RegExp | Array`。任何名称匹配的组件都不会被缓存； 
* max - `number | string`。最多可以缓存多少组件实例，一旦达到这个数 字，那么缓存组件中最近没有被访问的实例会被销毁；

**include 和 exclude  属性允许组件有条件地缓存：** 

* 二者都可以用<mark class="hltr-orange">逗号分隔字符串、正则表达式或一个数组</mark>来表示； 
* 匹配首先检查组件自身的 name 选项；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746867155000lp189r.png)

# 三、缓存组件的生命周期

对于缓存的组件来说，再次进入时，我们是<mark class="hltr-orange">不会执行created（组件创建完成）或者mounted（卸载组件）等生命周期函数</mark>的： 

* 但是有时候我们确实希望监听到何时重新进入到了组件，何时离开了组件； 
* 这个时候我们可以使用activated（活跃的） 和 deactivated（不活跃的） 这两个生命周期钩子函数来监听；
	* acrivated - 进入组件
	* deactivated - 离开组件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746867298000y538hr.png)


