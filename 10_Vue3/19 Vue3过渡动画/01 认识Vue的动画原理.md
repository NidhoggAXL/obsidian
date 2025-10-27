# 一、认识动画

在开发中，我们想要给一个组件的显示和消失添加某种过渡动画，可以很好的增加用户体验:

- React框架本身并没有提供任何动画相关的API，所以在React中使用过渡动画我们需要使用一个第三方库 [[01 React的过渡动画|react-transition-group]]
- Vue中为我们提供一些内置组件和对应的API来完成动画，利用它们我们可以方便的实现过渡动画效果

# 二、Vue的transition动画

Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡： 

* 条件渲染 (使用 v-if)条件展示 (使用 v-show) 
*  [[03 动态组件的使用|动态组件]]
* 组件根节点

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753419641000u9cqy6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534196460008br6it.png)

# 三、Transition组件的原理

会发现，Vue自动给h2元素添加了动画，这是什么原因呢？ 

当插入或删除包含在 transition 组件中的元素时，Vue 将会做以下处理： 

* 自动**嗅探目标元素是否应用了CSS过渡或者动画**，如果有，那么在恰当的时机添加/删除 CSS类名； 
* 如果 transition 组件**提供了JavaScript钩子函数**，这些钩子函数将在恰当的时机被调用；
* 如果没有找到JavaScript钩子并且也没有检测到CSS过渡/动画，DOM插入、删除操作将**会立即执行**；


