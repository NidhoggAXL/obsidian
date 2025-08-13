---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
1. 首先是通过ReactDom.createRoot获取根的React的DOM元素
2. 然后在根组件(root)使用render函数来渲染组件<App/>
3. React正常显式和渲染组件的内容
4. 当组件的button发生点击后，
5. 就会对btnClick进行回调（React会要对页面进行重新的渲染），
会回调这个函数，而React内部类似做
了下面的这种操作 ^JlgFe5D9

const click = this.btnClick ^9w4NqpkJ

click() ^i0OYLi6y

click()直接调用（函数直接调用）,那么根据this的绑定规则，click()函数
里面的this就不在是APP的实例对象，根据ES6的语法，在类里面的都是
编写的代码严格模式，同时使用 babel 转换的代码也是在严格模式下的 ，
this指向Window的在严格模式下就是undefined ^6q6WodVG


# Embedded files
abed20a6635a40b77311d0788f0530e85cf680d8: [[Pasted Image 20250810210545_025.png]]

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.10",
	"elements": [
		{
			"type": "image",
			"version": 152,
			"versionNonce": 1648941804,
			"isDeleted": false,
			"id": "T7tPe4xUZR2TDWKSsB11b",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -355.45524902442287,
			"y": -137.75588142141126,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 412.5398230088495,
			"height": 379,
			"seed": 196704876,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1754831739636,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "abed20a6635a40b77311d0788f0530e85cf680d8",
			"scale": [
				1,
				1
			]
		},
		{
			"type": "text",
			"version": 740,
			"versionNonce": 1345762156,
			"isDeleted": false,
			"id": "JlgFe5D9",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 70.44679937201397,
			"y": -139.73937001384633,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 585.615234375,
			"height": 161,
			"seed": 1219093740,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1754832929872,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "1. 首先是通过ReactDom.createRoot获取根的React的DOM元素\n2. 然后在根组件(root)使用render函数来渲染组件<App/>\n3. React正常显式和渲染组件的内容\n4. 当组件的button发生点击后，\n5. 就会对btnClick进行回调（React会要对页面进行重新的渲染），\n会回调这个函数，而React内部类似做\n了下面的这种操作",
			"rawText": "1. 首先是通过ReactDom.createRoot获取根的React的DOM元素\n2. 然后在根组件(root)使用render函数来渲染组件<App/>\n3. React正常显式和渲染组件的内容\n4. 当组件的button发生点击后，\n5. 就会对btnClick进行回调（React会要对页面进行重新的渲染），\n会回调这个函数，而React内部类似做\n了下面的这种操作",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "1. 首先是通过ReactDom.createRoot获取根的React的DOM元素\n2. 然后在根组件(root)使用render函数来渲染组件<App/>\n3. React正常显式和渲染组件的内容\n4. 当组件的button发生点击后，\n5. 就会对btnClick进行回调（React会要对页面进行重新的渲染），\n会回调这个函数，而React内部类似做\n了下面的这种操作",
			"lineHeight": 1.15,
			"baseline": 156
		},
		{
			"type": "text",
			"version": 201,
			"versionNonce": 292061140,
			"isDeleted": false,
			"id": "9w4NqpkJ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 73.0047545270341,
			"y": 38.86441772692913,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 249.70492553710938,
			"height": 25.776394273914267,
			"seed": 1357521132,
			"groupIds": [
				"Q6dFkIZ--eG3SQemrqldn"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1754831749960,
			"link": null,
			"locked": false,
			"fontSize": 22.414255890360234,
			"fontFamily": 2,
			"text": "const click = this.btnClick",
			"rawText": "const click = this.btnClick",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "const click = this.btnClick",
			"lineHeight": 1.15,
			"baseline": 20
		},
		{
			"type": "text",
			"version": 149,
			"versionNonce": 113211756,
			"isDeleted": false,
			"id": "i0OYLi6y",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 74.85057089235546,
			"y": 78.30902843311873,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 58.497894287109375,
			"height": 25.776394273914267,
			"seed": 586527700,
			"groupIds": [
				"Q6dFkIZ--eG3SQemrqldn"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1754831542832,
			"link": null,
			"locked": false,
			"fontSize": 22.414255890360234,
			"fontFamily": 2,
			"text": "click()",
			"rawText": "click()",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "click()",
			"lineHeight": 1.15,
			"baseline": 20
		},
		{
			"type": "text",
			"version": 619,
			"versionNonce": 2091783252,
			"isDeleted": false,
			"id": "6q6WodVG",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 73.87211068098242,
			"y": 126.23624846860059,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 645.60546875,
			"height": 92,
			"seed": 449803220,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1754981958122,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "click()直接调用（函数直接调用）,那么根据this的绑定规则，click()函数\n里面的this就不在是APP的实例对象，根据ES6的语法，在类里面的都是\n编写的代码严格模式，同时使用 babel 转换的代码也是在严格模式下的 ，\nthis指向Window的在严格模式下就是undefined",
			"rawText": "click()直接调用（函数直接调用）,那么根据this的绑定规则，click()函数\n里面的this就不在是APP的实例对象，根据ES6的语法，在类里面的都是\n编写的代码严格模式，同时使用 babel 转换的代码也是在严格模式下的 ，\nthis指向Window的在严格模式下就是undefined",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "click()直接调用（函数直接调用）,那么根据this的绑定规则，click()函数\n里面的this就不在是APP的实例对象，根据ES6的语法，在类里面的都是\n编写的代码严格模式，同时使用 babel 转换的代码也是在严格模式下的 ，\nthis指向Window的在严格模式下就是undefined",
			"lineHeight": 1.15,
			"baseline": 87
		},
		{
			"type": "rectangle",
			"version": 94,
			"versionNonce": 1151894764,
			"isDeleted": false,
			"id": "ROIp7RVw3N1mKtq47OTa6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 70.13706114515247,
			"y": 34.559829387366534,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 297.30467724656415,
			"height": 73.01297130941,
			"seed": 2051119828,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1754831758387,
			"link": null,
			"locked": false
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#e03131",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 2,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 2,
		"currentItemFontSize": 20,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 301.70578914454006,
		"scrollY": 536.031696904318,
		"zoom": {
			"value": 0.6990902649735019
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		}
	},
	"files": {}
}
```
%%