# 一、module的基本使用
什么是Module？ 

* 由于使用单一状态树，应用的所有状态会集中到一个比较大的对象，当应用变得非常复杂时，store 对象就有可能变得相当臃 肿； 
* 为了解决以上问题，Vuex 允许我们将 store 分割成<mark class="hltr-orange">模块（module）</mark>； 
* 每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747993777000ed7dhr.png)

# 二、module的局部状态
对于模块内部的 mutation 和 getter，接收的第一个参数是模块的局部状态对象：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748002979000pr9gdi.png)

> [!tip] 注意点：
> 当使用模块的时候，会把 getters、mutations、actions 都进行合并
> * 如果命名相同，就会存在问题，这是时候就需要使用module的命名空间
> * state 并<mark class="hltr-orange">不会进行合并</mark>，在使用 state 的时候需要指定模板，就不会存在重复

后面两个参数：

* 所有的 getters 方法
* 根的state

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748003392000apzm1v.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748003400000yoiz5h.png)

# 三、module的命名空间
默认情况下，模块内部的action和mutation仍然是<mark class="hltr-orange">注册在全局的命名空间</mark>中的： 

* 这样使得多个模块能够对同一个 action 或 mutation 作出响应；
* Getter 同样也默认注册在全局命名空间；

如果我们希望模块具有更高的封装度和复用性，可以添加 namespaced: true 的方式使其成为带命名空间的模块： 

* 当模块被注册后，它的所有 getter、action 及 mutation 都会自动根据模块注册的路径调整命名；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748003742000qas2vm.png)

> `{{ $store.getters["showName/showName`] }}
> * 第一个showName是在index.js里面module里面的名称![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748003875000vl9qic.png)
> * 第二个showName是show里面中getters的showName方法![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748003905000trrnhg.png)


# 四、module修改或派发根组件
如果我们希望在action中修改root中的state，那么有如下的方式：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17480049270001an81m.png)

  
