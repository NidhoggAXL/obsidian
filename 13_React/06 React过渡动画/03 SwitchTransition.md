SwitchTransition可以完成两个组件之间切换的炫酷动画：

- 比如我们有一个按钮需要在on和off之间切换，我们希望看到on先从左侧退出，off再从右侧进入； 
- 这个动画在vue中被称之为 [[04 动画的常见属性设置#三、过渡的模式mode(掌握)|vue transition modes]]； 
- react-transition-group中使用SwitchTransition来实现该动画；

SwitchTransition中主要有一个属性：**mode，有两个值**

- in-out：表示新组件先进入，旧组件再移除； 
- out-in：表示旧组件先移除，新组建再进入；

如何使用SwitchTransition呢？ 

- SwitchTransition组件里面要有CSSTransition或者Transition组件，不能直接包裹你想要切换的组件； 
- SwitchTransition里面的CSSTransition或Transition组件不再像以前那样接受in属性来判断元素是何种状态，取而代之的是 **key属性**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755324529000fh453k.png)

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175532476800055lrbw.png)

