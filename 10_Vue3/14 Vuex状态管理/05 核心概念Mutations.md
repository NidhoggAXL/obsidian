# 一、Mutation基本使用

更改 Vuex 的 store 中的状态的<mark class="hltr-cyan">唯一方法是提交 mutation</mark>：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747985748000lt39f6.png)

# 二、Mutation携带数据

很多时候我们在提交mutation的时候，会携带一些数据，这个时候我们可以**使用参数**：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747985788000he7o2s.png)

payload为对象类型

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747985798000e5yz4l.png)

对象风格的提交方式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747985807000eejwa2.png)

# 三、Mutation常量类型

定义常量：mutation-type.js

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747986188000sejzh4.png)

定义mutation：使用到 [[06 ES6对象的增强|计算属性名]]

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747986198000eo8uv2.png)

提交mutation

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479862510008mt0p4.png)

# 四、mapMutations辅助函数

也可以借助于辅助函数，帮助我们快速映射到对应的方法中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479871480001wox5h.png)

在setup中使用也是一样的：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747987184000pc82dm.png)

和前面使用 map 一样的，都可以自己使用 mapMutations
# 五、mutation重要原则

一条重要的原则就是要记住 mutation 必须是同步函数 

* 这是因为**devtool工具会记录mutation的日记**； 
* 每一条mutation被记录，**devtools都需要捕捉到前一状态和后一状态的快照**；
* 但是在mutation中执行异步操作，就无法追踪到数据的变化

所以Vuex的重要原则中要求 mutation 必须是同步函数； 

* 但是如果希望在Vuex中发送网络请求的话需要如何操作呢？




