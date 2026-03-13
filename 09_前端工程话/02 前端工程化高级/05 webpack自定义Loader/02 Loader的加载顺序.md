# 一、Loader的执行顺序

创建多个Loader使用，它的执行顺序是什么呢？ 从后向前、从右向左的

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773389069000shhr8q.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773389073000svetyr.png)

# 二、pitch-loader

事实上还有另一种Loader，称之为PitchLoader：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177338929400010ej5h.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773389306000vd0jo7.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773389354000rv9lfi.png)

其实这也是为什么loader的执行顺序是相反的：

 - run-loader先优先执行PitchLoader，在执行PitchLoader时进行loaderIndex++；
 - run-loader之后会执行NormalLoader，在执行NormalLoader时进行loaderIndex--；

# 三、enforce

那么，能不能改变它们的执行顺序呢？

 - 我们可以拆分成多个Rule对象，通过enforce来改变它们的顺序；

enforce一共有四种方式：

 - 默认所有的loader都是normal；
 - 在行内设置的loader是inline（import 'loader1!loader2!./test.js'）；
 - 也可以通过enforce设置 pre 和 post；

在Pitching和Normal它们的执行顺序分别是：

 - post, inline, normal, pre；
 - pre, normal, inline, post；

![gh|350](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773389622000y9qo6e.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773389647000i96t9t.png)


