# 一、认识前端路由

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755678727000c98wmi.png)

# 二、后端路由阶段

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755678762000f1p8e7.png)

# 三、前后端分离阶段

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755678824000k2ggqz.png)

# 四、URL的hash

前端路由是如何做到URL和内容进行映射呢？监听URL的改变。 

URL的hash 

- URL的hash也就是锚点(#), 本质上是改变window.location的href属性；
- 我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755678935000pkukd3.png)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556789390009lyhij.png)

> [!tip] hash的优势就是兼容性更好，在老版IE中都可以运行，但是缺陷是有一个#，显得不像一个真实的路径。

# 五、HTML5的History

history接口是HTML5新增的, 它有六种模式改变URL而不刷新页面：

- replaceState：替换原来的路径； 
- pushState：使用新的路径； 
- popState：路径的回退； 
- go：向前或向后改变路径； 
- forward：向前改变路径； 
- back：向后改变路径；

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755679025000qwybsm.png)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755679031000koja2q.png)

# 六、认识react-router

目前前端流行的三大框架, 都有自己的路由实现: 

- Angular的ngRouter 
- React的ReactRouter 
- Vue的[[02 Vue-Router基本使用|vue-router]]

React Router在最近两年版本更新的较快，并且React Router6.x版本中发生了较大的变化。 （2025年8月20日最新的React Router到7.x版本）

目前React Router6.x已经非常稳定，我们可以放心的使用； 

安装React Router6.x： 

- 安装时，我们选择react-router-dom； 
- react-router会包含一些react-native的内容，web开发并不需要；

```bash
npm install react-router-dom
```

安装React Router7.x，**在7版本中把前面的 react-router-dom等包都整合为一个 react-router 包了**： 

```bash
npm install react-router
```

React Router 6与7的区别:https://juejin.cn/post/7500939568200335400
