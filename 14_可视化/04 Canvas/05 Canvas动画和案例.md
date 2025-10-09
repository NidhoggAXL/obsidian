# 一、Canvas动画

Canvas绘图都是通过JavaScript 去操控的，如要实现一些交互性动画是相当容易的。那Canvas是如何做一些基本动画的？ 

- canvas可能最大的限制就是图像一旦绘制出来，它就是一直保持那样了。 
- 如需要执行动画，不得不对画布上所有图形进行一帧一帧的重绘（比如在1秒绘60帧就可绘出流畅的动画了）。 
- 为了实现动画，我们需要一些可以定时执行重绘的方法。然而在Canvas中有三种方法可以实现： 
	- 分别为 **setInterval** 、 **setTimeout** 和 **requestAnimationFrame** 三种方法来定期执行指定函数进行重绘

Canvas 画出一帧动画的基本步骤（如要画出流畅动画，1s 需绘60帧）： 

- 第一步：用 clearRect 方法清空 canvas ，**除非接下来要画的内容会完全充满 canvas（例如背景图），否则你需要清空所有**。 
- 第二步：保存 canvas 状态，如果加了 canvas 状态的设置（样式，变形之类的），又想在每画一帧之时都是原始状态的话， 你需要先保存一下，后面再恢复原始状态。 
- 第三步：绘制动画图形（animated shapes） ，即绘制动画中的一帧。 
- 第四步：恢复 canvas 状态，如果已经保存了 canvas 的状态，可以先恢复它，然后重绘下一帧。

# 二、绘制秒针- setInterval

绘制秒针动画，绘制一帧的步骤： 

- 第一步：用 clearRect(x,y, w,h)方法，清空 canvas 。 
- 第二步：保存 canvas 状态 。 
- 第三步：修改 canvas 状态 （样式、移动坐标、旋转等）。 
- 第四步：绘制秒针图形（即绘制动画中的一帧）。 
- 第五步：恢复 canvas 状态 ，准备重绘下一帧。


![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17583560880007xbppr.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758356099000fvptvd.png)


**setTimout定时器的缺陷** 

- setTimeout定时器不是非常精准的，因为setTimeout的回调函数是放到了[[03 宏任务、微任务队列|宏任务]]中等待执行。 
- 如果微任务中一直有未处理完成的任务，那么setTimeout的回调函数就有可能不会在指定时间内触发回调。 
- 如果想要更加平稳和更加精准的定时执行某个任务的话，可以使用**requestAnimationFrame函数**。

# 三、绘制秒针-requestAnimationFrame

## 3.1 什么是 requestAnimationFrame？

`requestAnimationFrame`（简称 rAF）是一个由浏览器专门为高性能动画提供的 API。它**通知浏览器您希望执行一个动画，并要求浏览器在下次重绘之前调用指定的函数来更新动画**。

它的核心思想是：**“与浏览器的渲染节奏保持同步”**。

## 3.2 为什么在 Canvas 中使用它？

在 Canvas 中制作动画（比如游戏、数据可视化）的传统方法是使用 `setInterval` 或 `setTimeout` 来周期性地调用绘制函数。例如：

```js
setInterval(() => {
  update(); // 更新逻辑
  draw();   // 绘制帧
}, 16); // 试图模拟 60fps (1000ms/60 ≈ 16ms)
```

这种方法有几个致命缺点：

1. **节奏不准**：JavaScript 计时器与屏幕刷新率不同步，可能导致掉帧或过度绘制（一帧内绘制了多次，但屏幕只刷新一次，浪费计算资源）。
    
2. **功耗问题**：即使页面被隐藏或最小化，计时器仍在运行，白白消耗 CPU 和电量。
    
3. **性能不佳**：浏览器无法优化计时器的执行时机。
    

`requestAnimationFrame` 完美地解决了这些问题：

1. **同步刷新**：它将回调函数的执行时机锁定在浏览器的每一次渲染之前，确保每秒执行次数与屏幕刷新率（<mark class="hltr-orange">通常</mark>是 60Hz，即 16.7ms/次）一致，无比流畅。
	- 实际调用次数取决于：
	    - 浏览器的刷新率
	    - JavaScript执行引擎的性能
	    - 系统负载等因素
    
2. **智能休眠**：当页面不可见（如切换了标签页或浏览器被最小化）时，`rAF` 会自动暂停调用，极大节省了系统资源。
    
3. **性能优先**：浏览器能根据系统负荷最优地安排动画的执行。


## 3.3 函数运行机制与时机图

`rAF` 的执行时机深深嵌入了浏览器的**渲染流水线**中。浏览器的一帧（Frame）内要完成很多工作，其简化时序图如下：

```text
-----------------------------------------------------------------------------------------------------
| Frame Start |   JavaScript (rAF callbacks)   |   Style   |   Layout   |   Paint   |   Composite   |
-----------------------------------------------------------------------------------------------------
              ^                                ^          ^            ^           ^               ^
              |                                |          |            |           |               |
              \-- 执行所有通过 rAF 注册的回调函数   /          |            |           |               |
                                       \-- 计算样式 --/           |            |           |               |
                                                \-- 计算布局 --/            |           |               |
                                                         \-- 生成绘制列表 --/           |               |
                                                                   \-- 绘制位图 --/               |
                                                                              \-- 合成层 --/
```

**详细流程解析：**

1. **一帧开始**：一个新的渲染周期开始。
    
2. **执行 rAF 回调**：这是 `requestAnimationFrame` 回调函数执行的**唯一时机**。在这个阶段，浏览器会执行所有在本轮渲染之前通过 `rAF` 注册的回调函数。
    
    - **你在回调函数里做什么？**：通常在这里更新你的动画状态（如物体的位置、速度）并调用 `canvas.drawImage()`、`canvas.fillRect()` 等方法来**重新绘制整个 Canvas 或其中变化的部分**。
        
3. **样式计算（Style）**：计算哪些 CSS 规则应用于哪些元素（这一步对常规 DOM 影响大，对纯 Canvas 影响较小）。
    
4. **布局（Layout）**：计算每个元素在屏幕上占据的几何空间和位置（回流）。
    
5. **绘制（Paint）**：填充像素的过程。对于 DOM，是生成元素的绘制列表。对于 Canvas，你之前在 `rAF` 回调中绘制的指令会在这里（或之后的复合阶段）被真正处理并输出到屏幕上。
    
6. **复合（Composite）**：将不同的层（包括 Canvas 层、DOM 层等）合并到一起，生成最终的屏幕图像。
    

> [!tip] **关键点：**
> - 你的**动画逻辑和绘制命令**必须赶在**Style-Layout-Paint**流程之前完成，也就是在 `rAF` 回调中完成。这样浏览器才能将你的新画面纳入本次渲染周期。
> 
> - 如果你在 `rAF` 之后（例如用 `setTimeout`）才修改样式或绘制，那么这个改动只能等到**下一个渲染周期**才会被绘制到屏幕上，导致动画延迟一帧，造成卡顿的感觉。


# 四、制作时钟

求圆上x, y的坐标： 

- 圆上x, y轴坐标实际上就是右图的 ( AB, BC )，AC为时钟半径 
- `x= AB = cosa * AC => x = Math.cos(弧度) * R` 
- `y= BC = sina * AC => y = Math.sin(弧度) * R` 
- 角度与弧度的 JS 表达式：`弧度=( Math.PI / 180 ) * 角度 => 弧度= 1角度对应的弧度 * 角度` 。 
- 比如：旋转90°：弧度为Math.PI / 2； 旋转180°：为Math.PI ； 旋转360°：为Math.PI * 2； 旋转-90°：为-Math.PI / 2； 
- 第 i 小时的坐标： 
	- `x = Math.cos( Math.PI * 2 / 12 * i ) * R`
	- `y = Math.sin( Math.PI * 2 / 12 * i ) * R`

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758392164000x9cd7q.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758392179000ntoi36.png)


绘制时钟，绘制一帧的步骤： 

- 第一步：用 clearRect(x,y, w,h)方法，清空 canvas 。 
- 第二步：保存 canvas 状态 。 
- 第三步：绘制白背景、绘制数字、绘制时/分/秒针、绘制圆、绘制时分刻度。 
- 第四步：恢复 canvas 状态 ，准备重绘下一帧。


<div style="
  height: 600px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758391844000a34gzw.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758391904000bgnfgm.png)


# 五、太阳系旋转

太阳系旋转动画，绘制一帧的步骤： 

- 第一步：用 clearRect(x,y, w,h)方法，清空 canvas ，并初始化全局样式。 
- 第二步：保存 canvas 状态 。 
- 第三步：绘制背景、绘制地球（绘制月球）、绘制阴影效果。
- 第五步：恢复 canvas 状态 ，准备重绘下一帧。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758392006000k7xtny.png)


<div style="
  height: 600px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1758391943000z0r5ob.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>


