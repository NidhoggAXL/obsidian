# 一、自定义connect


![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556697630005tu8eb.png)


![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755669769000gnxdjg.png)

# 二、context处理store

但是上面的connect函数有一个很大的缺陷：**依赖导入的store** 

- 如果我们将其封装成一个独立的库，需要依赖用于创建的 store，我们应该如何去获取呢？ 
- 难道让用户来修改我们的源码吗？不太现实； 

正确的做法是我们提供一个Provider，Provider来自于我们创建的Context，让用户将store传入到value中即可；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755669873000zwyxxu.png)

![gh|700](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755669879000xpgbef.png)

