# DefinePlugin的介绍
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744721288000km62ih.png)


# DefinePlugin的使用
DefinePlugin允许在编译时创建配置的全局常量，是一个webpack内置的插件（不需要单独安装）：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744721312000nb3ide.png)

这个时候，编译template就可以正确的编译了，会读取到**BASE_URL的值**；

# DefinePlugin的默认全局常量
DefinePlugin 有一个默认的全局常量：`process.env.NODE_ENV` 用来判断当前为什么开发环境？[[开发环境和生成环境]]

