# 一、lazy(懒惰)
lazy修饰符是什么作用呢？ 

* 默认情况下，v-model在进行双向绑定时，绑定的是 **input事件**，那么会在每次内容输入后就将最新的值和绑定的属性进行同 步； 
* 如果我们在v-model后跟上lazy修饰符，那么会将绑定的事件切换为 **change** 事件，只有在提交时（比如回车）才会触发；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746088724000v5r0du.png)

# 二、numble(数字

我们先来看一下v-model绑定后的值是什么类型的： 

* message<mark class="hltr-orange">总是</mark> **string类型**，即使在**我们设置type为number也是string类型**；
* 不管我们设置的类型是什么，v-model 也会默认为 **string类型

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746089571000mog57w.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746089468000k93m1b.png)

> 并且 message2 里面是**不可以输入数字之外的**


如果我们希望转换为数字类型，那么可以使用 **.number 修饰符：**

```html
<input type="text" v-model.number="score">
```

另外，在我们进行**逻辑判断**时，如果是一个**string类型**，在可以转化的情况下会进行**隐式转换**的： 

* 下面的score在进行判断的过程中会进行隐式转化的；
* 装换为 **num类型**
* 计算完成后就又是 **string类型**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1746089612000i6deue.png)

# 三、trim(修剪)

如果要自动过滤用户输入的守卫空白字符，可以给v-model添加 **trim 修饰符：**

```html
<input type="text" v-model.trim="message" />
```

# 四、多个修饰符联合使用

```html
<input type="text" v-model.lazy.trim="message" />
```

