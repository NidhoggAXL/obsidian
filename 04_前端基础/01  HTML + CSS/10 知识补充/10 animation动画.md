# 一、认识CSS Animation
**animation - 动画**

**CSS Animation的使用分成两个步骤:**

* **步骤一**:使用keyframes(关键帧)定义动画序列(每一帧动画如何执行)
* **步骤二**:配置动画执行的名称、持续时间、动画曲线、延迟、执行次数、方向等等

> [!tip] 重点
> animation 也是不会改变标准流的。
# 二、@keyframesguize
**可以使用@keyframes来定义多个变化状态，并且使用animation-name来声明匹配:**

* 关键帧使用 **percentage(百分比)** 来指定动画发生的时间点;
* **0%** 表示动画的第一时刻，**100%** 表示动画的最终时刻;
* 因为这两个时间点十分重要，所以还有特殊的别名:**from和to;**
	* form 相当于 0%
	* to 相当于 100%

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17252863540003c3s3e.png)


# 三、animation属性

**CSS animation 属性是 animation-name，animation-duration，animation-timing-function,，animation-delay，animation-iteration-count，animation-direction，animation-fill-mode 和 animation-play-state 属性的一个简写属性形式。**

**animation-name**:指定执行哪一个关键帧动画


**animation-duration**:指定动画的持续时间

* duration - 持续时间


**animation-timing-function**:指定动画的变化曲线

* timing - 时机
* function - 函数


**animation-delay**:指定延迟执行的时间

* delay - 延迟


**animation-iteration-count**:指定动画执行的次数，执行infinite表示无限动画

* iteration - 迭代/重复

**animation-direction**:指定方向，常用值normal和reverse

* direction - 方向

**animation-fill-mode**:执行动画最后保留哪一个值

* none:回到没有执行动画的位置
* forwards:动画最后一帧的位置
* backwards:动画第一帧的位置

|           |     |
| --------- | --- |
| fill      | 填满  |
| mode      | 模式  |
| forwards  | 向前  |
| backwards | 向后  |


**animation-play-state**:指定动画运行或者暂停(在JavaScript中使用，用于暂停动画)

* state - 状态


> [!tip] 简写属性
> ```css
> animation: name duration timing-function delay iteration-count direction fill-mode;
> ```
> 这些之间没有顺序，其中可以写多个值是定义中的`@keyframes`可以是多个，
> 比如：
> `animation:name……,name……;`


**代码示例：**

```html
<style>
	.box {
		display: inline-block;
		width: 200px;
		height: 200px;
		background-color: orange;
		animation: AXL 5s ease-in-out 2s 3 normal none;
	}
	@keyframes AXL {
		0% {
			transform: translate(0,0) scale(0.5,0.5);
		}
		20% {
			transform: translate(200px,0) scale(1,1);
		}
		50% {
			transform: translate(200px,100px) scale(0.2,0.2);
		}
		80% {
			transform: translate(0,100px) scale(1,1);
		}
		100% {
			transform: translate(0,50px) scale(1.5,1.5);
		}
	}
</style>

<div class="box"></div>
```





