# 一、认识粘性定位
**另外还有一个定位的值是position:sticky，比起其他定位值要新一些**

* 可以通过这个网站来查询那些浏览器兼容：caniuse.com
* sticky是一个大家期待已久的属性;
* 可以看做是**相对定位和固定(绝对)定位的结合体**
* 它允许被定位的元素**表现得像相对定位一样**，直到它滚动到某个值点
* 当达到这个阈值点时,就会变成固定(绝对)定位,

```html
<style>
	div {
		position: sticky;
		background-color: red;
		color: #ccc;
		top: 0;
	}
</style>

<h1>我是h1元素</h1>
<div>电脑|手机|手表</div>
<ul>

	<li>电脑1</li>

	<li>电脑2</li>

	<li>电脑3</li>

	<li>电脑4</li>

	<li>电脑5</li>

	<li>电脑6</li>

	<li>电脑7</li>

	<li>电脑8</li>

	<li>电脑9</li>

	<li>电脑10</li>

	<li>电脑11</li>

	<li>电脑12</li>

	<li>电脑13</li>

	<li>电脑14</li>

	<li>电脑15</li>

	<li>电脑16</li>

	<li>电脑17</li>

	<li>电脑18</li>

	<li>电脑19</li>

	<li>电脑20</li>

	<li>电脑21</li>

	<li>电脑22</li>

	<li>电脑23</li>

	<li>电脑24</li>

	<li>电脑25</li>

	<li>电脑26</li>

	<li>电脑27</li>

	<li>电脑28</li>

	<li>电脑29</li>

	<li>电脑30</li>

	<li>电脑31</li>

	<li>电脑32</li>

	<li>电脑33</li>

	<li>电脑34</li>

	<li>电脑35</li>

	<li>电脑36</li>

	<li>电脑37</li>

	<li>电脑38</li>

	<li>电脑39</li>

	<li>电脑40</li>

	<li>电脑41</li>

	<li>电脑42</li>

	<li>电脑43</li>

	<li>电脑44</li>

	<li>电脑45</li>

	<li>电脑46</li>

	<li>电脑47</li>

	<li>电脑48</li>

	<li>电脑49</li>

	<li>电脑50</li>

</ul>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723533926000ce2zxj.png)


**sticky是相对于最近的滚动祖先包含滚动视口的(the  nearest ancestor scroll container's scrollport)**

```html
<style>
	.box {
		width: 500px;
		height: 500px;
		margin: 100px auto 0;
		overflow: scroll;
	}
	.content {
		background-color: red;
		color: #ccc;
		position: sticky;
		top: 0;
	}
</style>

<body>
	<div class="box">
		<h1>我是h1元素</h1>
		<div class="content">
		电脑|手机|手表
		</div>
		<ul>
		
			<li>电脑1</li>
		
			<li>电脑2</li>
		
			<li>电脑3</li>
		
			<li>电脑4</li>
		
			<li>电脑5</li>
		
			<li>电脑6</li>
		
			<li>电脑7</li>
		
			<li>电脑8</li>
		
			<li>电脑9</li>
		
			<li>电脑10</li>
		
			<li>电脑11</li>
		
			<li>电脑12</li>
		
			<li>电脑13</li>
		
			<li>电脑14</li>
		
			<li>电脑15</li>
		
			<li>电脑16</li>
		
			<li>电脑17</li>
		
			<li>电脑18</li>
		
			<li>电脑19</li>
		
			<li>电脑20</li>
		
			<li>电脑21</li>
		
			<li>电脑22</li>
		
			<li>电脑23</li>
		
			<li>电脑24</li>
		
			<li>电脑25</li>
		
			<li>电脑26</li>
		
			<li>电脑27</li>
		
			<li>电脑28</li>
		
			<li>电脑29</li>
		
			<li>电脑30</li>
		
			<li>电脑31</li>
		
			<li>电脑32</li>
		
			<li>电脑33</li>
		
			<li>电脑34</li>
		
			<li>电脑35</li>
		
			<li>电脑36</li>
		
			<li>电脑37</li>
		
			<li>电脑38</li>
		
			<li>电脑39</li>
		
			<li>电脑40</li>
		
			<li>电脑41</li>
		
			<li>电脑42</li>
		
			<li>电脑43</li>
		
			<li>电脑44</li>
		
			<li>电脑45</li>
		
			<li>电脑46</li>
		
			<li>电脑47</li>
		
			<li>电脑48</li>
		
			<li>电脑49</li>
		
			<li>电脑50</li>
		
		</ul>
	</div>
</body>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1723534749000t4c0r7.png)







