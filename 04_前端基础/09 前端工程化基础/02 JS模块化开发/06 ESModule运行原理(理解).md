# 一、ES Module的解析流程
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744027252000g1zlpm.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744027256000q5qmx3.png)

# 二、阶段一：构建过程
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744177642000d8tav5.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744177647000quarvb.png)


# 三、阶段二和三：实例化阶段 – 求值阶段

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744027598000phrkmm.png)

> 要注意的是在**第二阶段实例化的时候**，只是在 Module Environment Record 里面做了一个记录，例如记录了：**count，还没有进行进行赋值**，只有到了**第三阶段才进行赋值的。**



