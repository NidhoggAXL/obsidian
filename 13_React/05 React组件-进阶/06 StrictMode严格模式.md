# 一、StrictMode

StrictMode 是一个用来突出显示应用程序中潜在问题的工具： 

- 与 Fragment 一样，StrictMode 不会渲染任何可见的 UI； 
- 它为其后代元素触发额外的检查和警告； 
- 严格模式检查仅在开发模式下运行；它们**不会影响生产构建**；

可以为应用程序的任何部分启用严格模式： 

- 不会对 Header 和 Footer 组件运行严格模式检查； 
- 但是，ComponentOne 和 ComponentTwo 以及它们的所有后代元素都将进行检查；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755309743000b1l9c5.png)

# 二、严格模式检查的是什么？

1. 识别不安全的生命周期：

2. 使用过时的 ref API

3. 检查意外的副作用
   - 这个组件的 constructor 会被调用两次；
   - 这是严格模式下故意进行的操作，让你来查看在这里写的一些逻辑代码被调用多次时，是否会产生一些副作用；
   - 在生产环境中，是否会被调用两次的；

4. 使用废弃的 findDOMNode 方法
   - 在之前的 React API 中，可以通过 findDOMNode 来获取 DOM，不过已经不推荐使用了，可以自行学习演练一下

5. 检测过时的 context API
   - 早期的 Context 是通过 static 属性声明 Context 对象属性，通过 getChildContext 返回 Context 对象等方式来使用 Context 的；
   - 目前这种方式已经不推荐使用，大家可以自行学习了解一下它的用法；



