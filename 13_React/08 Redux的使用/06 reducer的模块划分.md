# 一、Reducer代码拆分

先来理解一下，为什么这个函数叫reducer？ 

看一下目前我们的reducer： 

- 当前这个reducer有处理cotegories的的代码
- 后续cotegories相关的状态状态会进一步变得更加复杂； 
- 也会继续添加其他的相关状态，比如购物车、分类、歌单等等； 
- 如果将所有的状态都放到一个reducer中进行管理，随着项目的日趋庞大，必然会造成代码臃肿、难以维护。

因此，我们可以对reducer进行拆分： 

- 先抽取一个对cotegories处理的reducer； 
- 再抽取一个对hotSuggestion处理的reducer； 
- 将它们合并起来；

# 二、Reducer文件拆分

目前我们已经将不同的状态处理拆分到不同的reducer中，我们来思考： 

- 虽然已经放到不同的函数了，但是这些函数的处理依然是在同一个文件中，代码非常的混乱； 
- 另外关于reducer中用到的constant、action等我们也依然是在同一个文件中；

![gh|300](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755609115000zrq185.png)

# 三、combineReducers函数

目前合并的方式是通过每次调用reducer函数自己来返回一个新的对象。 

事实上，redux给我们提供了一个combineReducers函数可以方便的让我们对多个reducer进行合并：combine - 结合

> [!ps]
> 将处理的 reducer 和 aciton 都进行一个导出，但是不会在这里再创建store，`const store = createStore(reducer)` 。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556093260003qb6hm.png)

> [!ps]
> 
> 将所有的 reducer 放到统一的一个地方进行创建store，对多个reducer创建到一个Store中。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755609171000o6swot.png)

> [!abstract]
> categoriesReducer使用：
> 
> - 前面对所有的action都进行了导出，那么在组件中，谁用到了某个aciton，只要进行导入就可以啦。
> - 所有的reducer到统一进行创建到一个Store中啦，那么就会保存到同一个state中，需要使用到那一个数据，只需要到对应state对应的reducer中去获取就可以啦。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556094130004oyprt.png)

那么combineReducers是如何实现的呢？ 

- 事实上，它也是**将传入的reducers合并到一个对象中，最终返回一个combination的函数（相当于我们之前的reducer函数了）**； 
- 在执行combination函数的过程中，它会通过**判断前后返回的数据是否相同来决定返回之前的state还是新的state**； 
- 新的state会触发订阅者发生对应的刷新，而旧的state可以有效的组织订阅者发生刷新；



