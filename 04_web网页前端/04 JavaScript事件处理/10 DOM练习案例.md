# 一、轮播消息提示


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728654673000w18za3.png)

**每过 3 秒，图片和内容会进行替换**
 
style:

```html
<style>
body {
  text-align: center;
}

.tip-bar {
  display: inline-flex;
  flex-direction: row;
  align-items: center;
  height: 30px;
  background-color: rgba(0,0,0,.4);
  border-radius: 16px;
  margin-top: 20px;
}

img {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  margin-right: 5px;
}

span {
  font-size: 13px;
  color: white;
  margin-right: 8px;
}
</style>
```

body:

```html
<body>
  <div class="tip-bar">
    <img src="https://bfs.biyao.com/group1/M01/A2/67/rBACVGA_iOuAYaTxAAAPbted3yE165.png" alt="">
    <span>183***138对这件商品感兴趣</span>
  </div>
  
  <script>
    let tipList = [
      {
        icon: 'https://bfs.biyao.com/group1/M01/A6/97/rBACYWBCHqyAFH5tAAANZXX5Eww646.png',
        title: 'coderwhy对这件商品感兴趣'
      },
      {
        icon: 'https://bfs.biyao.com/group1/M01/A2/67/rBACVGA_iOuAYaTxAAAPbted3yE165.png',
        title: '123***814对这件商品感兴趣'
      },
      {
        icon: 'https://bfs.biyao.com/group1/M00/7F/4E/rBACYV16HseAP-PnAAAW9bbVoKE463.png',
        title: '刘军对这件商品感兴趣'
      }
    ]

    var divEl = document.querySelector(".tip-bar")
    var imgEl = divEl.querySelector("img")
    var spanEl = divEl.querySelector("span")

    var index = 0
    setInterval(function() {
      imgEl.src = tipList[index].icon
      spanEl.textContent = tipList[index].title
      index++
      if (index === tipList.length) {
        index = 0
      }
    },3000)
  </script>
</body>
```



# 二、关闭隐藏消息

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17286565320007anmd5.png)

**点击 x 区域的时候会把整个 元素全部隐藏掉。**

style：

```html
<style>
.top-bar {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 45px;
  width: 375px;
  background-color: black;
  /* 关键 */
  overflow: hidden;
  transition: all .3s ease-out;
}

.delete {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 30px;
  cursor: pointer;
}

.delete img {
  height: 10px;
  width: 10px;
}

.logo {
  height: 30px;
  width: 30px;
  margin-left:3px;
  margin-right: 30px;
  cursor: pointer;
}

span {
  color: white;
  font-size: 14px;
  flex: 1;
  
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.btn {
  width: 94px;
  height: 100%;
  line-height: 45px;
  text-align: center;
  font-size: 14px;
  color: #fff;
  background-color: #F63515;
}

</style>
```


body：

```js
<body>
  <div class="top-bar">
    <div class="delete">
      <img src="./img/delete.png" alt="">
    </div>
    <img class="logo" src="./img/logo.png" alt="">
    <span>打开京东App,购物更轻松</span>
    <div class="btn">立即打开</div>
  </div>

  <script>
    var barEl = document.querySelector(".top-bar")
    var deleteEl = barEl.querySelector(".delete")
  
    //对点击的 div.delete 进行监听
    deleteEl.onclick = function() {
      //通过高度来进行改变，让改变的更加自然
      //使用transition来进行过渡
      barEl.style.height = 0
    }

    // 过渡动画监听器
    barEl.ontransitionend = function() {
      barEl.remove()
    }
    //这样分开来监听的好处就是，当动画结束的时候才进行remove操作
  </script>
</body>
```


那么如果同时在 deleteEl 上面进行改变高度和remover操作呢？

```js
<script>
	var barEl = document.querySelector(".top-bar")
	var deleteEl = barEl.querySelector(".delete")
	
	//对点击的 div.delete 进行监听
	deleteEl.onclick = function() {
	  //通过高度来进行改变，让改变的更加自然
	  //使用transition来进行过渡
	  barEl.style.height = 0
	  barEl.remove()
	}
<script>
```

这样的话，动画的过渡效果会有 3 秒钟，我们过渡动画中高度的改变还没有完成的时候，remove() 操作就已经进行了

这样的话我们就会看不到过渡的动画

# 三、侧边栏展示
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728809464000wjzu4g.png)

当我们移动鼠标到图标上面的时候，前面的内容会有一个从左向右的显示出来。

```html
  <div class="tool-bar">
    <div class="item">
      <i class="icon"></i>
      <div class="name">购物车</div>
    </div>
    <div class="item">
      <i class="icon"></i>
      <div class="name">收藏</div>
    </div>
    <div class="item">
      <i class="icon"></i>
      <div class="name">限时活动</div>
    </div>
    <div class="item">
      <i class="icon"></i>
      <div class="name">大礼包</div>
    </div>
  </div>
```

```js
<script>
	// 1.获取元素
	var iconEls = document.querySelectorAll(".icon")
	var itemEls = document.querySelectorAll(".item")
	
	// 2.动态设置icon对用精灵图的位置（有规律）
	for (var i = 0; i < iconEls.length; i++) {
	  var iconEl = iconEls[i]
	  iconEl.style.backgroundPosition = `-48px -${i*50}px`
	}
	
	for (var itemEl of itemEls) {
	  itemEl.onmouseenter = function() {
		this.children[1].style.width = "64px"
	  }
	  itemEl.onmouseleave = function() {
		this.children[1].style.width = "0"
	  }
	}
</script>
```

# 四、tab切换实现
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17288015410003j96nx.png)

当一个被选中的时候，其他的不被选中（排他思想）

```js
<div class="tab_control">
	<div class="item active">精品栏目</div>
	<div class="line"></div>
	<div class="item">赛事精品</div>
	<div class="line"></div>
	<div class="item">英雄攻略</div>
</div>

<script>
	var tabEl = document.querySelector(".tab_control")
	var activeEl = document.querySelector(".active")
	//拿到事件发生的对象
	tabEl.onmouseover = function(event) {
	  var itemEl = event.target
	  console.log(itemEl)
	  if (itemEl.classList.contains("item")) {
		activeEl.classList.remove("active")
		itemEl.classList.add("active")
		activeEl = itemEl
	  }
	}
</script>
```

# 五、王者荣耀轮播图
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1728801788000t8v19o.png)

```html
<div class="main main_wrapper">
	<div class="news-section">
		<div class="banner">
			<ul class="img-list">
				<li class="item">
					<a href="#" >
						<img src="./img/banner_01.jpeg" alt="#">
					</a>
				</li>
				<li class="item">
					<a href="#" >
						<img src="./img/banner_01.jpeg" alt="#">
					</a>
				</li>
				<li class="item">
					<a href="#" >
						<img src="./img/banner_01.jpeg" alt="#">
					</a>
				</li>
				<li class="item">
					<a href="#" >
						<img src="./img/banner_01.jpeg" alt="#">
					</a>
				</li>
				<li class="item">
					<a href="#" >
						<img src="./img/banner_01.jpeg" alt="#">
					</a>
				</li>
			</ul>
			<ul class="title-list">
				<li class="item active">
					<a href="#" >
						桑起的旅游故事
					</a>
				</li>
				<li class="item">
					<a href="#" >
						桑起的旅游走心
					</a>
				</li>
				<li class="item">

					<a href="#" >

						桑起的旅游开始

					</a>

				</li>

				<li class="item">

					<a href="#" >

						桑起的旅游过程

					</a>

				</li>

				<li class="item">

					<a href="#" >

						桑起的旅游结束

					</a>

				</li>

			</ul>

		</div>

	</div>

</div>
```

```js
<script>
	var titleEl = document.querySelector(".title-list")
	var activeTitleEl = titleEl.querySelector(".active")
	var bannerEl = document.querySelector(".banner")

	var imglistEl = document.querySelector(".img-list")
	var imgToggle = 0
	var timeID = null

	//文字对应图片
	titleEl.onmouseover = function(event) {
		var textEl = event.target.parentElement
		if (textEl.classList.contains("active")) return
		//找到文字对应的索引
		for(var index = 0; index < titleEl.children.length; index++) {
			if (titleEl.children[index] === textEl) break
		}
		imgToggle = index
		switchBanner()
	}

	//添加轮播定时器
	startTime()

	//封装轮播效果
	function switchBanner() {
		imglistEl.style.transform = `translateX(${-604 * imgToggle}px)`
		imglistEl.style.transition = `all 300ms ease`
		activeTitleEl.classList.remove("active")
		var imgListToggle = titleEl.children[imgToggle]
		imgListToggle.classList.add("active")
		activeTitleEl = imgListToggle
	}

	bannerEl.onmouseenter = function() {
		clearInterval(timeID)
	}
	bannerEl.onmouseleave = function() {
		startTime()
	}

	//添加定时器函数
	function startTime() {
		timeID = setInterval(function() {
			imgToggle++
			if (imgToggle === imglistEl.children.length) {
				imgToggle = 0
			}
			switchBanner()
		}, 2000)
	}
</script>
```

# 六、购物车操作案例


添加功能购买数量中的增量和减少购买数量,


