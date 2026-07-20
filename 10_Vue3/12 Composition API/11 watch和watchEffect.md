# 一、监听数据的变化

在前面的Options API中，我们可以通过[[04 监听器watch选项使用|watch]]选项来侦听data或者props的数据变化，当数据变化时执行某一些操作。 

在Composition API中，我们可以使用watchEffect和watch来完成响应式数据的侦听； 

* watchEffect：用于**自动收集响应式数据**的依赖； 
* watch：需要**手动指定侦听**的数据源；

# 二、watch的使用

watch的API完全等同于组件watch选项的Property： 

* watch需要**侦听特定的数据源**，并且**执行其回调函数**； 
* 默认情况下它是[[惰性和急切|惰性]]的，只有当被侦听的源发生变化时才会执行回调；

```js
import { ref, watch } from 'vue'

const name = ref("kobe")

watch(name, (newValue, oldValue) => {
    console.log(newValue, oldValue);
})

const changeName = () => {
    name.value = "james";
}
```


# 三、侦听多个数据源

侦听器还可以使用数组同时侦听多个源：

```js
const name = ref("why");
const age = ref(18);

const changeName = () => {
    name.value = "james";
}

watch([name, age], (newValues, oldValues) => {
    console.log(newValues, oldValues);
})
```

# 四、watch的选项

如果我们希望侦听一个深层的侦听，那么依然需要设置 deep 为true： 

* 也可以传入 immediate 立即执行；

```js
const info = reactive({
  name: "why",
  age: 18,
  friend: {
    name: "kobe"
  }
})

watch(info, (newValue, oldValue) => {
  console.log(newValue, oldValue)
}, { immediate: true, deep: true })
)
```


也可以编写为一个函数，这样默认就是**深层监听**（算深层监听的一种语法糖）：

```js
const info = reactive({
  name: 'why',
  age: 18,
  friend: {
    name: 'kobe'
  }
})

watch(() => info, (newValue, oldValue) => {
  console.log(newValue, oldValue)
})
```
# 五、watchEffect

当侦听到某些响应式数据变化时，我们希望执行某些操作，这个时候可以使用watchEffect。

**我们来看一个案例：** 

* 首先，watchEffect传入的函数会被**立即执行一次**，并且在执行的过程中会收集依赖； 
* 其次，只有收集的依赖发生变化时，watchEffect传入的函数才会再次执行；

```js
const name = ref("why");
const age = ref(18);

watchEffect(() => {
    console.log("watchEffect执行~", name.value, age.value);
})
```


> [!node]
> 
> 例如上面的例子：这里的依赖就是 name 和 age

# 六、watchEffect的停止侦听

如果在发生某些情况下，我们希望停止侦听，这个时候可以获取watchEffect的返回值函数，调用该函数即可。 

比如在上面的案例中，我们age达到20的时候就停止侦听：

```js
const stopWatch = watchEffect(() => {
  console.log("watchEffect执行~", name.value, age.value);
});

const changeAge = () => {
  age.value++;
  if (age.value > 20) {
    stopWatch();
  }
};
```

