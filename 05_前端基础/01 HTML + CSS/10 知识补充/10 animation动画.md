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

animation的组成属性

| 属性                          | 作用           | 默认值       |
| --------------------------- | ------------ | --------- |
| `animation-name`            | 指定关键帧动画的名称   | `none`    |
| `animation-duration`        | 动画完成一个周期所需时间 | `0s`      |
| `animation-timing-function` | 动画的速度曲线      | `ease`    |
| `animation-delay`           | 动画开始前的延迟时间   | `0s`      |
| `animation-iteration-count` | 动画播放次数       | `1`       |
| `animation-direction`       | 动画是否反向播放     | `normal`  |
| `animation-fill-mode`       | 动画执行前后如何应用样式 | `none`    |
| `animation-play-state`      | 动画运行或暂停      | `running` |
|                             |              |           |

##  3.1 animation-name

定义要应用的`@keyframes`动画名称。

```css
animation-name: slide-in;
```

## 3.2 animation-duration

定义动画完成一个周期所需时间，单位可以是秒(s)或毫秒(ms)。


```css
animation-duration: 2s;
```

## 3.3 animation-timing-function

定义动画的速度曲线：

- `ease` - 慢快慢（默认）
    
- `linear` - 匀速
    
- `ease-in` - 慢开始
    
- `ease-out` - 慢结束
    
- `ease-in-out` - 慢开始和结束
    
- `cubic-bezier(n,n,n,n)` - 自定义贝塞尔曲线
    
- `steps(n)` - 分步动画


```css
animation-timing-function: ease-in-out;
```


## 3.4 animation-delay

定义动画开始前的等待时间。

```css
animation-delay: 1s;
```

## 3.5 animation-iteration-count

定义动画播放次数：

- `n` - 具体次数
    
- `infinite` - 无限循环

```css
animation-iteration-count: 3;
```

## 3.6 animation-direction

定义动画播放方向：

- `normal` - 正常播放
    
- `reverse` - 反向播放
    
- `alternate` - 正反交替
    
- `alternate-reverse` - 反正交替

```css
animation-direction: alternate;
```

## 3.7 animation-fill-mode

定义动画执行前后如何应用样式：

- `none` - 不应用任何样式
    
- `forwards` - 保持最后一帧样式
    
- `backwards` - 应用第一帧样式（含延迟）
    
- `both` - 同时应用forwards和backwards

```css
animation-fill-mode: forwards;
```

## 3.8 animation-play-state

控制动画运行状态：

- `running` - 运行中
    
- `paused` - 暂停

```css
animation-play-state: paused;
```

## animation简写语法

```css
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
```

> [!warning] **注意**
> 简写属性中，只有`animation-duration`和`animation-delay`的值是时间类型，且顺序固定（duration在前，delay在后）。

简写实例：

```css
/* 只指定必要属性 */
animation: slide-in 2s;

/* 包含更多属性 */
animation: slide-in 2s ease-in-out 1s infinite alternate;

/* 完整属性 */
animation: slide-in 2s linear 0.5s 3 normal forwards running;
```

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


## 多动画声明

```css
animation: 
    slide-in 2s ease-in-out,
    fade-out 1.5s linear 0.5s;
```







