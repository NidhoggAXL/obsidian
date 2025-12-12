# 一、URL传递

```html
<navigator url="/pages/about/about?name=axl&age=18">about</navigator>


<script setup>
import { onLoad } from "@dcloudio/uni-app"

//方式一：Vue的defineProps函数
const props = defineProps({
	name: {
		type: String
	},
	age: {
		type: String
	}
})
console.log(props);

//方式二：uni的页面周期
onLoad((option) => {
	console.log("onLoad 接收数据：", option);
})
</script>
```

# 二、eventChannel

```js
<script setup>
function handleBtn() {
	uni.navigateTo({
		url: "/pages/prifix/prifix",
		success(res) {
			res.eventChannel.emit("aboutData", {
				data: "我是about里面的数据"
			})
		}
	})
}
</script>
```

```js
// 接收数据
<script setup>
import { getCurrentInstance, ref } from 'vue';
import { onLoad } from "@dcloudio/uni-app"

	// 就是获取vue组件的实例 === this
	const $instance = ref(getCurrentInstance().proxy)
	onLoad((option) => {
		const eventChannel = $instance.value.getOpenerEventChannel()
		eventChannel.on("aboutData", (value) => {
			console.log(value);
		})
	})
</script>
```

# 三、事件总线

```html
// 发送数据
<template>
	<view>
		about02
		<button type="default" @click="handleBtn()">about01</button>
	</view>
</template>

<script setup>
	function handleBtn() {
		uni.navigateTo({
			url: "/pages/about02/about02"
		})
		uni.$emit("about01", {
			data: "about01的数据"
		})
	} 
</script>
```


```html
// 接收数据
<template>
	<view>
		about01
		<navigator url="/pages/about02/about02">about02</navigator>
	</view>
</template>

<script setup>
	import { onLoad, onUnload } from "@dcloudio/uni-app"
	onLoad(() => {
		uni.$on("about01", getAbout02)
	})
	onUnload(() => {
		uni.$off("about01", getAbout02)
	})
	
	function getAbout02(value) {
		console.log("about02的数据", value);
	}
	
</script>
```


