# 认识模块热替换(HMR)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17447243900009c2moq.png)

# 开启HMR
修改 webpack.config.js 的配置(**默认是开启的**)：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744724498000zq8hhz.png)

浏览器可以看到如下效果：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744724528000x9hygc.png)

但是你会发现，当我们修改了某一个模块的代码时，依然是刷新的整个页面： 

* 这是因为我们需要去指定哪些模块发生更新时，进行HMR；
* 一班在开发环境中，是对 **总入口文件** 进行设置编写

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744724928000a644gh.png)

这个时候修改 bar.js 就会进行热模块修改，并不会刷新整个页面

* 先判断 module.hot 是否开启热模块
* 修改了 bar.js 会进行回调

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174472502500059u40o.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725034000wpnl85.png)


# 框架的HMR
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725651000s9v6rk.png)

# host配置

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725672000qvr5d6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17447257040000vjpun.png)

# port、open、compress(了解)
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17447257260003lsndo.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725730000uuvkva.png)

# Vue项目阶段
## Proxy（Vue项目学习）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725749000ov32gm.png)

## changeOrigin的解析（Vue项目学习）
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725765000ij7ntm.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725769000vn9gvh.png)

## historyApiFallback （Vue项目学习）
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744725787000k96g2x.png)

