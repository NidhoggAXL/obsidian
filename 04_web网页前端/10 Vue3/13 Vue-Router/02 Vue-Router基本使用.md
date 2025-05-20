# 一、认识vue-router

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17476622300009133y5.png)

# 二、hash路由模式使用
使用vue-router的步骤: 

* **第一步**：创建路由需要映射的组件（打算显示的页面）；![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747662393000q1mxnv.png)
 
* **第二步**：通过createRouter创建路由对象，并且传入routes和history模式； 
	* 配置路由映射: 组件和路径映射关系的routes数组； 
	* 创建基于hash或者history的模式； ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747662787000eyq67n.png)
* **第三步**：使用app注册路由对象（use方法）； ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747662970000tu02op.png)
* **第四步**：路由使用: 通过`<router-link>`和`<router-view>`![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747663414000tq8k4r.png)![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17476634950006jf8b5.png)

如下面界面，如果点击 Home 或者 About ，就会改变 URL 的 hash 值，并且会显示对应的组件。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747663810000pt3stk.png)


# 三、路由的默认路径
我们这里还有一个不太好的实现: 

* 默认情况下, 进入网站的首页, 我们希望渲染首页的内容； 
* 但是我们的实现中, **默认没有显示首页组件, 必须让用户点击才可以**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747664322000k9uwih.png)

如何可以让路径默认跳到到首页, 并且`<router-view>`渲染首页组件呢?

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747664440000k1gyjt.png)

我们在routes中又配置了一个映射： 

* path配置的是根路径: `/` 
* <mark class="hltr-orange">redirect是重定向</mark>, 也就是我们将根路径<mark class="hltr-orange">重定向到/home的路径下</mark>, 这样就可以得到我们想要的结果了.

# 四、history路由模式使用

另外一种选择的模式是history模式：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747665366000i6hazs.png)

这样的话再进行路由的时候URL就不会存在`#`号：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747665575000wu2j36.png)

# 五、router-link

router-link事实上有很多属性可以配置： 

* to属性： 
	* 是一个字符串，或者是一个对象 
	* 目的确定占位路由是哪一个

 * replace属性： 
	 * 设置 replace 属性的话，当点击时，会调用 router.replace()，而不是 router.push()； 
	 * 目的是不记录历史记录，当点击返回的时候会直接回到浏览器搜索页面
	 
 * active-class属性： 
	 * 设置激活a元素后应用的class，默认是router-link-active 
	 * 如果添加的 active-class 就会替换掉 router-link-active 的 class![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17477238300005sucie.png)
	 
 * exact-active-class属性：[[04 动态路由和路由嵌套#6.1 精准路由|路由嵌套的精准路由]] 
	 * 链接精准激活时，应用于渲染的`<a>`的 class，默认是router-link-exact-active；

