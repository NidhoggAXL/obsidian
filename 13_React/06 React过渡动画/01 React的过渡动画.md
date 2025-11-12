# 一、react-transition-group介绍

在开发中，我们想要给一个组件的显示和消失添加某种过渡动画，可以很好的增加用户体验。 

当然，我们可以通过原生的CSS来实现这些过渡动画，但是React社区为我们提供了react-transition-group用来完成过渡动画。 

React曾为开发者提供过动画插件 react-addons-css-transition-group，后由社区维护，形成了现在的 react-transition-group。

- 这个库可以帮助我们方便的实现组件的 **入场** 和 离场 **动画**，使用时需要进行额外的安装：

```bash
#npm
npm install react-transition-group --save

# yarn 
yarn add react-transition-group
```

>[!tip] 
>
>react-transition-group本身非常小，不会为我们应用程序增加过多的负担。

# 二、react-transition-group主要组件

react-transition-group主要包含四个组件： 

**Transition** 

- 该组件是一个和平台无关的组件（不一定要结合CSS）； 
- 在前端开发中，我们一般是结合CSS来完成样式，所以比较常用的是CSSTransition；

**CSSTransition** 

- 在前端开发中，通常使用CSSTransition来完成过渡动画效果 

**SwitchTransition** 

- 两个组件**显示和隐藏**切换时，使用该组件 

**TransitionGroup** 

- 将多个动画组件包裹在其中，一般用于列表中元素的动画；





