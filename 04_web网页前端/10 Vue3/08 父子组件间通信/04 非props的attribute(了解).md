# 一、非Prop的Attribute

什么是非Prop的Attribute呢？ 

* 当我们传递给一个组件某个属性，但是该属性<mark class="hltr-orange">并没有定义对应的props或者emits时</mark>，就称之为 非Prop的Attribute； 
* 常见的包括class、style、id属性等；

Attribute继承 

* 当组件有单个根节点时，非Prop的Attribute将自动添加到根节点的Attribute中：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17462827720009czatc.png)


# 二、禁用Attribute继承和多根节点

如果我们<mark class="hltr-yellow">不希望组件的根元素继承attribute</mark>，可以在组件中设置<mark class="hltr-orange"> inheritAttrs: false</mark>

* 禁用attribute继承的常见情况是需要将attribute应用于根元素之外的其他元素；
* 我们可以通过 `$attrs`来访问所有的 非props的attribute；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/174628285100076i3uj.png)

**多个根节点的attribute** 

* 多个根节点的attribute如果没有显示的绑定，那么会报警告，我们<mark class="hltr-orange">必须手动的指定</mark>要绑定到哪一个属性上：


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746282879000afgex4.png)




