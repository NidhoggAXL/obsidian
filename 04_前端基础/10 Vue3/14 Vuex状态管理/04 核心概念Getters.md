# 一、getters基本使用

某些属性我们可能需要经过变化后来使用，这个时候可以使用getters：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479802100004go5ar.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747980179000nvso3y.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479801860004mertj.png)

# 二、getters第二个参数
getters可以接收第二个参数：第二个参数主要是接收 getters ，并可以根据这个参数使用 getters 的其他方法。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747980541000mkx31b.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747980549000mu7smj.png)

# 三、getters的返回函数
getters中的函数本身，可以返回一个函数，那么在使用的地方相当于可以调用这个函数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17479812890006tcb66.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747981296000iq9ivu.png)


# 四、mapGetters的辅助函数

也可以使用mapGetters的辅助函数。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747984856000yo290c.png)

在setup中使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747984864000yjrtxk.png)

当然也可以是和[[03 核心概念State#3.1 解构和toRef结合使用(推荐)| state ]]一样使用 toRefs 来进行响应式处理更加方便

也可以使用下面的操作：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174798516600031gm8z.png)







