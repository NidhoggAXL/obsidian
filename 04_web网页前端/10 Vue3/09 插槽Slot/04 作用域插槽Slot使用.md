# 一、渲染作用域
在Vue中有渲染作用域的概念： 

* 父级模板里的所有内容都是在<mark class="hltr-orange">父级作用域中编译</mark>的； 
* 子模板里的所有内容都是在<mark class="hltr-orange">子作用域中编译</mark>的；

如何理解这句话呢？我们来看一个案例： 

* 在我们的案例中ChildCpn自然是可以让问自己作用域中的title内容的； 
* 但是在App中，是访问不了ChildCpn中的内容的，因为它们是跨作用域的访问；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17467899540002acatm.png)

# 二、作用域插槽
**但是有时候我们希望插槽可以访问到子组件中的内容是非常重要的：** 

* 当一个组件被用来渲染一个<mark class="hltr-orange">数组元素时</mark>，我们使用插槽，并且希望插槽中显示每项的内容； 
* 这个Vue给我们提供了作用域插槽；

我们来看下面的一个案例： 

* 在App.vue中定义好数据 
* 传递给ShowNames组件中 
* ShowNames组件中遍历names数据 
* 定义插槽的prop 
* 通过v-slot:default的方式获取到slot的props
* 使用slotProps中的item和index

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174679067600091o1ug.png)

# 三、独占默认插槽的缩写

如果我们的插槽是默认插槽default，那么在使用的时候 `v-slot:default="slotProps"`可以简写为 `v-slot="slotProps"：`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746791196000c1ktmp.png)

并且如果我们的插槽只有默认插槽时<mark class="hltr-orange">(一个插槽)</mark>，<mark class="hltr-orange">组件的标签可以被当做插槽的模板来使用</mark>，这样，我们就可以将 v-slot 直接用在组件上：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746791247000h2bszt.png)


# 四、默认插槽和具名插槽混合

但是，如果我们有默认插槽和具名插槽，那么按照完整的template来编写。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746791297000a0iyeo.png)

只要出现多个插槽，请始终为所有的插槽使用完整的基于`<tempalte>语法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746791325000dipilt.png)




