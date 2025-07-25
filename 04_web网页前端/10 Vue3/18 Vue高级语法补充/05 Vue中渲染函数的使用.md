# 一、认识h函数

Vue推荐在绝大数情况下使用模板来创建你的HTML，然后一些特殊的场景，你真的需要J**avaScript的完全编程的能力**，这个时 候你可以使用 **渲染函数** ，它比模板更接近**编译器**；

前面我们讲解过[[11 Vue的虚拟DOM#一、认识VNode|VNode]]和[[11 Vue的虚拟DOM|VDOM]]的概念： 

* Vue在生成真实的DOM之前，会将**我们的节点转换成VNode**，而VNode组合在一起形成**一颗树结构**，就是虚拟DOM （VDOM）； 
* 事实上，我们之前编写的 template 中的HTML 最终也是使用**渲染函数生成对应的VNode**； 
* 那么，如果你想充分的利用JavaScript的编程能力，我们可以自己来编写 **createVNode 函数，生成对应的VNode**；

那么我们应该怎么来做呢？使用 h()函数： 

* h() 函数是一个用于**创建 vnode 的一个函数**； 
* 其实更准备的命名是 **createVNode() 函数**，但是为了简便在Vue将之**简化为 h() 函数**；

# 二、h()函数 如何使用呢？
h()函数 如何使用呢？它接受三个参数：

1. 第一个参数
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753411253000199xcu.png)
2. 第二个参数
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753411277000hfx7k9.png)
3. 第三个参数
	![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753411298000aij4iw.png)

> [!tip] 注意事项： 
> * 如果没有props，那么通常可以将children作为第二个参数传入； 
> * 如果会产生歧义，可以将null作为第二个参数传入，将children作为第三个参数传入；

# 三、h函数的基本使用

h函数可以在两个地方使用： 

* render函数选项中； 
* setup函数选项中（setup本身需要是一个函数类型，函数再返回h函数创建的VNode）；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753411470000wsfq3i.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/175341147500032spjv.png)

# 四、h函数计数器案例

## 4.1 Opsiton API

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753411888000952z88.png)

```js
<script>
import { h } from 'vue';

export default {
  data() {
    return {
      count: 0
    }
  },
  render() {
    return h('div', { class: 'app' }, [
      h('h1', '使用函数式组件'),
      h('p', `当前计数: ${this.count}`),
      h('button', {
        onClick: () => {
          this.count += 1
        }
      }, '增加计数'),
      h('button', {
        onClick: () => {
          this.count -= 1
        }
      }, '减少计数'),
    ])
  }
}
</script>
```

## 4.2 Composition API

不使用 setup 语法糖编写：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753412217000595w5y.png)

使用 setup 语法糖编写：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753412710000g2o01t.png)

