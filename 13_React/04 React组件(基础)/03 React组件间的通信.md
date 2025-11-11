# 一、组件之间嵌套

组件之间存在嵌套关系： 

- 在之前的案例中，只是创建了一个组件App； 
- 如果一个应用程序将所有的逻辑都放在一个组件中，那么这个组件就会变成非常的臃肿和难以维护； 
- 所以组件化的核心思想应该是对组件进行拆分，拆分成一个个小的组件； 
- 再将这些组件组合嵌套在一起，最终形成应用程序；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755083032000ww7q68.png)

上面的嵌套逻辑如下，它们存在如下关系： 

- App组件是Header、Main、Footer组件的父组件； 
- Main组件是Banner、ProductList组件的父组件；

# 二、认识组件间的通信

在开发过程中，会经常遇到需要组件之间相互进行通信： 

- 比如App可能使用了多个Header，每个地方的Header展示的内容不同，那么我们就需要使用者传递给Header一些数据，让其进行展示； 
- 又比如我们在Main中一次性请求了Banner数据和ProductList数据，那么就需要传递给他们来进行展示； 
- 也可能是子组件中发生了事件，需要由父组件来完成某些操作，那就需要子组件向父组件传递事件； 

总之，在一个React项目中，组件之间的通信是非常重要的环节；

父组件在展示子组件，可能会传递一些数据给子组件： 

- 父组件通过 **属性=值** 的形式来传递给子组件数据； 
- 子组件通过 **props** 参数获取父组件传递过来的数据；

# 三、父组件传递子组件

## 3.1 类组件和函数组件

> [!tip] Recat 内部给把 props 通过 super(props) 在类组件里面进行了一个保存，类似在constructor里面 `this.props = props` 的操作。


<div style="
  height: 700px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755084146000yvhshu.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>

## 3.2 参数propTypes

**从 React v15.5 开始，React.PropTypes 已移入另一个包中：prop-types 库**

```bash
npm install prop-sypes
```

**React 19 不建议使用这个，建议使用 TypeScript 来代替**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755089342000jw4zv6.png)

对于传递给子组件的数据，有时候我们可能希望进行验证，特别是对于大型项目来说： 

- 当然，如果你项目中默认继承了Flow或者TypeScript，那么直接就可以进行类型验证； 
- 但是，即使我们没有使用Flow或者TypeScript，也可以通过 prop-types 库来进行参数验证； 


更多的验证方式，可以参考官网：

- https://zh-hans.reactjs.org/docs/typechecking-with-proptypes.html 
- 比如验证数组，并且数组中包含哪些元素； 
- 比如验证对象，并且对象中包含哪些key以及value是什么类型； 
- 比如某个原生是必须的，使用 requiredFunc: PropTypes.func.isRequired

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755089197000gqr4lx.png)

# 四、子组件传递父组件

某些情况，我们也需要子组件向父组件传递消息： 

- 在vue中是通过自定义事件来完成的； 
- 在React中同样是通过props传递消息，只是让父组件给子组件传递一个回调函数，在子组件中调用这个函数即可；

我们这里来完成一个案例： 

- 将计数器案例进行拆解； 
- 将按钮封装到子组件中：AppChlidren； 
- AppChlidren，将内容传递到父组件中，修改counter的值；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755095122000l9lvlu.png)


