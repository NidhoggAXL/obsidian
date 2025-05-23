# 一、如何使用Pinia
使用Pinia之前，我们需要先对其进行安装：

```bash
yarn add pinia
npm install pinia
```

创建一个pinia并且将其传递给应用程序

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748006911000618tgf.png)

# 二、认识Store

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748006933000pp5r5g.png)

# 三、定义一个Store
定义一个Store： 

* 我们需要知道 Store 是<mark class="hltr-orange">使用 defineStore() 定义</mark>的，
* 并且它需要一个<mark class="hltr-orange">唯一名称</mark>，作为第一个参数传递（类似ID）；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748007139000hte7hk.png)

> [!tip] 重点：
> * <mark class="hltr-orange">defineStore 返回的是一个函数</mark>，这也是 composition API 方便使用的
> * 这个 name，也称为 id，<mark class="hltr-orange">是必要的</mark>，Pinia 使用它来将 store 连接到 devtools。
>  * 返回的函数<mark class="hltr-orange">统一使用useX作为命名方案</mark>，这是约定的规范；
> 	 * use + name 使用小驼峰命名

# 四、使用定义的Store

Store在它被使用之前是不会创建的，我们可以通过调用<mark class="hltr-orange">use函数</mark>来使用Store：

* 使用的时候不需要再确定使用 counter 里面的什么属性（`counter.state.count`)，直接使用就可以啦（`counter.count`)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17480082080005nwf7p.png)

注意Store获取到后不能被解构，那么会失去响应式： 

* 为了从 Store 中提取属性同时保持其响应式，您需要使用<mark class="hltr-orange">storeToRefs()</mark>。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748008826000rs9p8r.png)

