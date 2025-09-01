# 一、React更新机制

React的渲染流程：

> jsx -> 虚拟DOM -> 真实DOM

那么React的更新流程呢？

> props/state改变 -> render函数重新执行 -> 产生新的虚拟DOM树 -> 新旧虚拟DOM树更新 -> 计算出差异进行更新 -> 更新到真实DOM


# 二、React的更新流程

React在props或state发生改变时，会调用React的render方法，会创建一颗不同的树。 

**React需要基于这两颗不同的树之间的差别来判断如何有效的更新UI：** 

- 如果一棵树参考另外一棵树进行完全比较更新，那么即使是最先进的算法，该算法的复杂程度为 O(n³)，其中 n 是树中元素的数量； 
- 如果在 React 中使用了该算法，那么展示 1000 个元素所需要执行的计算量将在十亿的量级范围； 
- 这个开销太过昂贵了，React的更新性能会变得非常低效；

**于是，React对这个算法进行了优化，将其优化成了O(n)，如何优化的呢？**

- 同层节点之间相互比较，**不会垮节点比较**； 
- **不同类型的节点，产生不同的树结构**；
- 开发中，可以通过key来指定哪些节点在不同的渲染下保持稳定；

# 三、keys的优化

我们在前面遍历列表时，总是会提示一个警告，让我们加入一个key属性：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755175711000wkbpll.png)

**方式一**：在最后位置插入数据 

- 这种情况，有无key意义并不大 

**方式二**：在前面插入数据 

- 这种做法，在没有key的情况下，所有的li都需要进行修改； 

**当子元素(这里的li)拥有 key 时，React 使用 key 来匹配原有树上的子元素以及最新树上的子元素：** 

- 在下面这种场景下，key为111和222的元素仅仅进行位移，不需要进行任何的修改； 
- 将key为333的元素插入到最前面的位置即可； 

**key的注意事项**： 

- key应该是**唯一**的； 
- key**不要使用随机数**（随机数在下一次render时，会重新生成一个数字）； 
- 使用**index作为key**，对性能是**没有优化**的；

# 四、render函数被调用

我们使用之前的一个嵌套案例： 

- 在App中，我们增加了一个[[04 React其他案例实现#二、计数器|计数器的代码]]； 
- 当点击+1时，会重新调用App的render函数； 
- 而当App的render函数被调用时，**所有的子组件的render函 数都会被重新调用**；

那么，我们可以思考一下，在以后的开发中，我们只<mark class="hltr-orange">要是修改了 App中的数据，所有的组件都需要重新render</mark>，进行diff算法， 性能必然是很低的：

- 事实上，很多的组件没有必须要重新render； 
- 它们调用render应该有一个前提，就是依赖的数据（state、 props）发生改变时，再调用自己的render方法；

如何来控制render方法是否被调用呢？ 通过shouldComponentUpdate方法即可；

# 五、shouldComponentUpdate

React给我们提供了一个生命周期方法 <mark class="hltr-orange">shouldComponentUpdate（很多时候，我们简称为SCU）</mark>，这个方法接受参数，并且需要有 返回
![[02 React组件生命周期#2.4 不常用生命周期函数|shouldComponentUpdate]]

**比如我们在App中增加一个message属性：** 

- jsx中并没有依赖这个message，那么它的改变不应该引起重新渲染；
- 但是因为render监听到state的改变，就会重新render，所以最后render方法还是被重新调用了；

> [!tip] 数据少的时候还可以使用一下 shouldComponentUpdate ，但是一但数据多，这是一个极其疯狂的事情，需要对每一个组件都进行设置，这是不可能的。

# 六、PureComponent

如果所有的类，我们都需要手动来实现 shouldComponentUpdate，那么会给我们开发者增加非常多的工作量。 

- 我们来设想一下shouldComponentUpdate中的各种判断的目的是什么？ 
- **props或者state中的数据是否发生了改变**，决定shouldComponentUpdate返回true或者false； 

事实上React已经考虑到了这一点，所以React已经默认帮我们实现好了，如何实现呢？ 

* 将class继承自PureComponent。
* 是一个<mark class="hltr-orange">浅层比较</mark>


```jsx
import React, { PureComponent } from 'react'

export class Home extends PureComponent {
  render() {
    console.log("Home render")
    return (
      <div>Home</div>
    )
  }
}

export default Home
```

## 6.1 案例

**错误编写：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755180410000z2ighk.png)

**正确编写：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755215007000w6436t.png)


![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755215326000nalffh.png)

## 6.1 shallowEqual方法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551783790004y4ewp.png)

这个方法中，调用 `!shallowEqual(oldProps, newProps) || !shallowEqual(oldState, newState)`，这个shallowEqual就是 进行浅层比较：

- 比如两个对象和数组，都**不对深层里面的数据比较**，而是比较在内存中新旧地址是否相同，

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17551787750000sjuxz.png)

# 七、高阶组件memo

目前我们是针对类组件可以使用PureComponent，那么函数式组件呢？

- 事实上函数式组件我们在props没有改变时，也是不希望其重新渲染其DOM树结构的

我们需要使用一个高阶组件memo： 

- 我们将之前的Header、Banner、ProductList都通过memo函数进行一层包裹； 
- Footer没有使用memo函数进行包裹； 
- 最终的效果是，当counter发生改变时，Header、Banner、ProductList的函数不会重新执行； 
- 而Footer的函数会被重新执行；

```jsx
import React, { memo } from 'react'

const Banner = memo(
  function Banner() {
    return (
      <div>Banner</div>
    )
  }
)

export default Banner
```

# 八、不可变数据的力量

要修改 this.state 里面的数据，都需要进行一个拷贝在操作，操作附件，完成后再把附件赋值给 this.state 。

就算是深层的内容改变，也要先进行拷贝，操作附件，<mark class="hltr-orange">这种不可以对原数据的直接改变的方式就成为不可变数据的力量。</mark>




