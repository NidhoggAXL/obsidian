使用到的知识点：[[06 类型工具和类型体操#2.11 InstanceType`<Type>`|instaceType]]

```ts
type 组件类型你 = instaceType<typeof 组件名>
```

为什么可以这样使用？

Vue中组件是返回一个对象：

```js
<script>
export default {
  data: () => ({}),
  methods: {},
  setup: {}
  //其他逻辑
}
</script>
```

> [!warning]
> 虽然是返回一个对象，但是这个对象本质可以看作是一个类，当在 template 中使用组件的时候，实质是使用这个类创建一个实例，没使用一次就是创建一个实例。

```html
import About form './About.vue'

//template中使用
<About />
<About />

//使用了两次就是创建了两个实例
```




