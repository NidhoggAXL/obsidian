# 一、Mustache语法绑定
WXML基本格式:

- 类似于HTML代码:比如可以写成单标签，也可以写成双标
- 必须有严格的闭合:没有闭合会导致编译错误
- **大小写敏感**:class和Class是不同的属性

开发中,界面上展示的数据并不是写死的,而是会根据服务器返回的数据，或者用户的操作来进行改变

- 如果使用原生JS或者jQuery的话,我们需要通过操作DOM来进行界面的更新
- 小程序和Vue一样,提供了插值语法: Mustache语法(双大括号)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/175361698000065tjku.png)

# 二、WXML的条件渲染

## 2.1 wx:if、wx:elif、wx:else
某些时候, 我们需要根据条件来决定一些内容是否渲染： 

- 当条件为true时, view组件会渲染出来 
- 当条件为false时, view组件不会渲染出来

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753617255000fkh5vm.png)

## 2.2 hidden属性
hidden属性: (默认为true)

- hidden是所有的组件都默认拥有的属性； 
- 当hidden属性为true时, 组件会被隐藏； 
- 当hidden属性为false时, 组件会显示出来；

```html
<view hidden="{{false}}">哈哈</view>
```

hidden和wx:if的区别 

- hidden控制隐藏和显示是控制是否添加hidden属性 
- wx:if是控制组件是否渲染的
# 三、WXML的列表渲染

## 3.1 wx:for基础

为什么使用wx:for？  

* 在实际开发中，服务器经常返回各种**列表数据**，我们不可能一一从列表中取出数据进行展示； 
* 需要通过for循环的方式，遍历所有的数据，一次性进行展示；

在组件中，我们可以使用wx:for来遍历一个**数组 （字符串 - 数字）、对象**

- 默认情况下，遍历后在wxml中可以使用一个**变量index**，保存的是当前遍历数据的下标值。 
- 数组中对应某项的数据，使用**变量名item**获取。

```html
<!-- 遍历数组 -->
<view wx:for="{{['a', 'b', 'c', 'd', 'e', 'f']}}">{{item}}-{{index}}</view>
item 对应的是每次遍历的数据，index %% 对应的是索引

<!-- 遍历字符串 -->

<view wx:for="{{'hello axl'}}">{{item}}</view>
item 对应的是每次遍历得到的 单字符，index 对应索引

<!-- 遍历数字 -->
<view wx:for="{{10}}">{{item}}</view>
item 对应的是每次遍历得到的 前面一个数字+1（默认第一个是 0），index 对应索引

<!-- 遍历对象 -->
<view wx:for="{{name:'axl',age: '18'}}">{{item}}-{{index}}</view>
item 对应对象的是 value，index 对应的是 key
```

## 3.2 block标签
什么是block标签？ 

* 某些情况下，我们需要使用 wx:if 或 wx:for时，可能需要包裹一组组件标签 
- 我们希望对这一组组件标签进行整体的操作，这个时候怎么办呢？

> [!important] 注意：`<block />` 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。


使用block有两个好处： 

- 将需要进行遍历或者判断的内容进行包裹。
- 将遍历和判断的属性放在block便签中，不影响普通属性的阅读，提高代码的可读性。

## 3.3 item/index名称
默认情况下，item – index的名字是**固定**的 

- 但是某些情况下，我们可能想**使用其他名称** 
- 或者当出现**多层遍历时**，名字会重复 

这个时候，我们可以指定item和index的名称：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753621050000vprsz8.png)

## 3.4 key作用

我们看到，使用wx:for时，会报一个警告： 

- 这个提示告诉我们，可以添加一个**key来提供性能**。 

为什么需要这个key属性呢？ 

- 这个其实和小程序内部也使用了**虚拟DOM有关系**（和Vue、React很相似）。 
- 当某一层有很多相同的节点时，也就是列表节点时，我们希望插**入、删除一个新的节点，可以更好的复用节点**； 

wx:key 的值以两种形式提供 

- 字符串，代表在 for 循环的 array 中 **item 的某个 property**，该 property 的值需要是列表中**唯一的字符串或数字**，且不能 **动态改变**。 
- 保留关键字 `*this` 代表在 for 循环中的 **item 本身**，这种表示需要 item 本身是一个唯一的字符串或者数字。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753621395000bi6bav.png)


