# 编写案例
我们创建一个 div_ct.js ,通过JavaScript创建了一个元素，并且希望给它设置一些样式；

* 通过 impot 导出，在导入文件数据不使用的时候可以省略 export 
* `export {} from impot ""`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744358442000lfp8cp.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744358453000ycwb63.png)

文件所处于的文件夹：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744358500000ht3zoc.png)


继续编译命令`npx webpack`：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744358673000p7ttns.png)


# css-loader的使用
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744546946000b4vzae.png)


# css-loader的使用方案

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744547006000bkg28o.png)


# loader配置方式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17445473810004kfscg.png)

# loader的配置代码
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744547527000tkuvhj.png)

# 认识style-loader

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744547664000ax9xfc.png)


# 配置style-loader
那么我们应该如何使用style-loader： 

* 在配置文件中，添加style-loader； 

> [!tip] 注意：
>因为loader的执行顺序是从右向左（或者说从下到上，或者说从后到前的），所以我们需要将style-loader写到cssloader的前面；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17445477340006qgcao.png)

重新执行编译 **npx webpack**，可以发现打包后的css已经生效了： 

* 当前目前我们的css是通过页内样式的方式添加进来的； ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744548512000dpcjny.png)

* 后续我们也会讲如何将css抽取到单独的文件中，并且进行压缩等操作；

**最后在在html中引入打包好的文件就好了：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744548426000a76gz2.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744548438000nzv5qi.png)



