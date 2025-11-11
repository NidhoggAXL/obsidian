# 一、组件化开发

整个逻辑其实可以看做一个整体，那么就可以将其封装成一个组件： 

- **root.render 参数**是一个**HTML元素**或者**一个组件**； 
- 所以可以先将之前的业务逻辑封装到**一个组件**中，然后传入到 ReactDOM.render 函数中的第一个参数；

在React中，如何封装一个组件呢？这里暂时使用类的方式封装组件： 

- 定义一个类（**类名大写，组件的名称是必须大写的，小写会被认为是HTML元素**），继承自React.Component 
- **实现当前组件的render函数** 
	- render当中返回的jsx内容，就是之后React会帮助我们渲染的内容

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754828641000z1kiii.png)

# 二、数据依赖

在组件中的数据，可以分成两类： 

- **参与界面更新的数据**：当数据变量时，需要更新组件渲染的内容； 
- **不参与界面更新的数据**：当数据变量时，不需要更新将组建渲染的内容； 

参与界面更新的数据我们也可以称之为是**参与数据流**，这个数据是定义在当前对象的state中 

- 可以通过在构造函数中 **this.state = {定义的数据}** 
- 在 constructor 里面必须调用 [[02 extends实现继承#二、super关键字|super()]] 函数。
- 当数据发生变化时，可以**调用 this.setState 来更新数据**，并且通知React进行update操作； 
	- 在进行update操作时，就会**重新调用render函数**，并且使用最新的数据，来**渲染界面**
	- 这就是为什么要是使用 this.setState 来改变数据了，使用 this.state 来改变数据，那么组件并不会重新渲染(**执行render函数**)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754830679000m16gfq.png)

# 三、事件绑定

**事件绑定中的this** ： 在类中直接定义一个函数，并且将这个函数绑定到**元素的onClick事件**上，当前这个函数的this指向的是谁呢？ 

默认情况下是**undefined** 

- 很奇怪，居然是undefined； 
- 因为在正常的DOM操作中，监听点击，监听函数中的this其实是节点对象（比如说是button对象）； 
- 这是因为React并不是直接渲染成真实的DOM，我们所编写的button只是一个语法糖，它的本质React的Element对象； 
- 那么在这里发生监听的时候，**react在执行函数时并没有绑定this，默认情况下就是一个undefined**；

![[React的事件绑定this|100%]]

**我们在绑定的函数中，可能想要使用当前对象，比如执行 this.setState 函数，就必须拿到当前对象的this** 

- 我们就需要在传入函数时，给这个函数直接绑定this 
- 类似于下面的写法：`<button onClick={this.btnClick.bind(this)}>改变文本</button>`
- 为什么使用 [[01 this的绑定规则|bind]] 呢，是因为**bind可以永久绑定**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754832188000i4hddv.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17548322640002wyuzj.png)

如果有多个元素，都是使用到这个 btnClik 的实例方法，那么编写起来就会太麻烦啦，每次都要使用 bind 进行绑定，所有就有了下面这种编写方式：

- 提前对 btnClik 进行正确的绑定，并添加到 App 实例属性中，直接调用属性方法。
- 在构造的 constructor 的时候就进行一个绑定。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1754832507000qfianj.png)



