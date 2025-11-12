CSSTransition是基于Transition组件构建的：

CSSTransition执行过程中，有三个状态：appear(出现)、enter(进入)、exit(退出)； 

**它们有三种状态，需要定义对应的CSS样式：** 

- 第一类，**开始状态**：对于的类是-appear、-enter、exit； 
- 第二类：**执行动画**：对应的类是-appear-active、-enter-active、-exit-active； 
- 第三类：**执行结束**：对应的类是-appear-done、-enter-done、-exit-done；

**CSSTransition常见对应的属性：** 

- in：触发进入或者退出状态
	- 如果添加了**unmountOnExit={true}**，那么该组件**会在执行退出动画结束后被移除掉**； 
	- **当in为true时，触发进入状态**，会添加-enter、-enter-acitve的class开始执行动画，当动画执行结束后，会移除两个class， 并且添加-enter-done的class； 
	- **当in为false时，触发退出状态**，会添加-exit、-exit-active的class开始执行动画，当动画执行结束后，会移除两个class，并 且添加-enter-done的class；
- classNames：动画class的名称 
	- 决定了在编写css时，对应的class名称：比如card-enter、card-enter-active、card-enter-done；
- timeout：过渡动画的时间
- appear： 是否在初次进入添加动画（需要和in同时为true）
- **unmountOnExit**：退出后卸载组件 
- 其他属性可以参考官网来学习： 
	- https://reactcommunity.org/react-transition-group/transition 
- CSSTransition对应的钩子函数：主要为了检测动画的执行过程，来完成一些JavaScript的操作 
	- onEnter：在进入动画之前被触发； 
	- onEntering：在应用进入动画时被触发； 
	- onEntered：在应用进入动画结束后被触发；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755314652000ba43ab.png)


```jsx
import React, { PureComponent, createRef } from 'react'
import { CSSTransition } from 'react-transition-group';

export class App extends PureComponent {
  constructor() {
    super()
    this.state = {
      isShow: true
    }
    // 创建 ref
    this.nodeRef = createRef(null)
  }

  render() {
    const { isShow } = this.state
    return (
      <div>
        <CSSTransition
          in={isShow}
          nodeRef={this.nodeRef}  // 添加 nodeRef
          classNames='axl'
          unmountOnExit={true}
          timeout={2000}
          appear
        >
          <div ref={this.nodeRef}>  {/* 将 ref 附加到 DOM 元素 */}
            <h2>你的名字</h2>
            <p>在开发中，我们想要给一个组件的显示和消失添加某种过渡动画，可以很好的增加用户体验。</p>
          </div>
        </CSSTransition>
      </div>
    )
  }
}

export default App
```



