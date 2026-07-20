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

unref

 - 如果我们想要获取一个ref引用中的value，那么也可以通过unref仿法:
 - 如果参数是一个ref，则返回内部值，否则返回参数本身;
 - 这是 `val =isRef(val)?val.value:val` 的语法糖函数;

isRef：判断值是否是一个ref对象。

shallowRef：创建一个浅层的ref对象;

triggerRef：手动触发和shallowRef相关联的副作用:

```js
const info = shallowRef({name: "axl"})

// 下面的修改不是响应式的
const changeInfo = () => {
  info.value.name = "coderaxl"
  // 手动触发
  triggerRef(info)
}
```



