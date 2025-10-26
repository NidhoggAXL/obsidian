# 一、toRefs

如果我们使用ES6的解构语法，对reactive返回的对象进行解构获取值，那么之后无论是修改结构后的变量，还是修改reactive，返回的state对象，**数据都不再是响应式**

```js
const state = reactive({
  name: "why",
  age: 18
})

const { name, age } = state
```

那么有没有办法让我们解构出来的属性是响应式的呢?

 - Vue为我们提供了一个toRefs的函数，可以将reactive返回的对象中的属性都转成ref
 - 那么**再次进行结构出来的 name 和 age 本身都是 ref 响应式的**

```js
//但我们这样来进行操作的时候，会返回两个ref对象，它们是响应式的
const { name, age } = toRefs(state)
```

> [!abstract]
> 
> 这种做法相当于已经在 **state.name和ref.value之间建立了链接**，任何一个修改都会引起另外一个变化;

# 二、toRef

如果只希望转换一个reactive对象中的属性为ref,那么可以使用toRef的方法:

```js
const name = toRef(state, "name")
```

# 三、ref其他的API

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747557609000yr4i4t.png)


