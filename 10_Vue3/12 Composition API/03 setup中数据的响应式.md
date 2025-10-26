# 一、Reactive API

如果想为在setup中定义的数据提供**响应式**的特性，那么我们可以使用**reactive的函数**：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747550407000z719sd.png)

那么这是什么原因呢?为什么就可以变成响应式的呢?

- 这是因为当使用reactive函数处理我们的数据之后数据**再次被使用时就会进行依赖收集**
- 当数据发生改变时，所有收集到的依赖都是进行对应的响应式操作(比如更新界面)
- <mark class="hltr-cyan">事实上，编写的data选项，也是在内部交给了reactive函数将其编程响应式对象的;</mark>


# 二、Ref API

reactive API对传入的类型是有限制的，它要求必须传入的是一个对象或者数组类型

- 如果传入一个基本数据类型(String、Number、Boolean)会报一个警告

```bash
value cannot be made reactive: Hello World
值无法被定义为reactive(响应式): Hello World
```

这个时候Vue3给我们提供了另外一个API: `ref AP`

- ref 会返回一个可变的响应式对象，该对象作为一个 **响应式的引用** 维护着它内部的值，这就是ref名称的来源
- 它<mark class="hltr-cyan">内部的值是在ref的 value 属性中被维护的;</mark>

```js
import { ref } from "vue"
const message = ref("Hello World")
```

> [!tip] 这里有两个注意事项:
>
 > - 在模板中引入ref的值时，Vue会自动帮助进行解包操作，所以并不需要在模板中通过 ref.value 的方式来使用
 >
 > - 但是在 setup 函数内部，它依然是一个ref引用，所以对其进行操作时，我们依然需要使用 ref.value 的方式

# 三、Ref自动解包

模板中的解包是浅层的解包，在下面这种情况下，就必须要使用 ref.value 的方式。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17475506570005241s8.png)


如果我们将ref放到一个reactive的属性当中时，那么在模板中使用时，它会自动解包：

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747550716000hssrab.png)


# 四、开发中reactive和ref选择

reactive的应用场景

* 条件一:reactive应用于本地的数据
* 条件二:多个数据之间是有关系和联系(聚合的数据，组织在一起会有特定的作用)

**例如用户名和密码就应该使用reactive来使用，这些数据都是具有一定的联系的。**

ref的应用场景:

* 其他的场景基本都用ref和[[07 computed函数使用|computed]]
* 定义本地的一些简单数据
* 定义从网络中获取的数据也是使用ref
