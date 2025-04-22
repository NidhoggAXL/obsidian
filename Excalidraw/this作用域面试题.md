---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
等价与 person1的属性
foo1里面的
function () {
    console.log(this.name)
}

person1.fool() 等价与 fn() ^26YgbynY

function () {
    console.log(this.name)
} 
例如上面等于的匿名函数为fn
注意不是fn()，有小括号就是执行了这个函数 ^tQoVVb54

等价与 fn.call(person2) ^y3udzeP1

等价与
foo1: fn ^1KiPgV28

等价于
foo3: function () {
    return fn
} ^NdxNM3Bm

等价与  fn
有()说明执行了函数，
但是里面的return了 fn
所以就等价与 fn ^MTcWp6El

等价与 fn() ^oCtCnq3o

person1.foo3.call(person2) 表示打印的话
foo3: function () {
    console.log (this)// person2
    return fn
}
调用了foo3方法，return得到 fn
函数内部存在this，call 显式绑定了person2

person.foo3.call(person2)()
这个表示的就是fn(),执行了foo3属性的方法，
返回了fn，后面()在执行返回的函数就是fn() ^rgRLipi8

默认绑定 ^Vtmxo5pn

person1.foo3() 等价与 fn
执行了foo3的方法，return 了fn

person1.foo3().call(person2) = fn.call(person2)
这是一个显示绑定，对返回的fn的一个绑定调用
所以显式绑定 - person2  ^29virnGI

等价于放回的箭头函数 wn ^SHUuSF6M

() => {
    console.log(this.name)
}
例如上面的箭头函数为wn
注意不是wn()，有小括号就是执行了这个函 ^oLnRem64

等价于 wn() ^hdsyD5jr

person1.foo4.call(person2) 表示打印的话
foo4: funtion () {
    console.log(this) //person2
    reurn wn
}
调用了foo4方法，return得到wn
函数内部存在this，call 显式绑定了person2

person1.foo4.call(person2)() 等价与 wn()

wn是一个箭头函数里面this作用域，向外找到外层的
函数内部显式绑定的 person2 ^xgbC6oiJ

person1.foo4()等价于 wn
() 说明调用了foo4的方法 ，通过return返回了 wn

person1.foo4().call(person2) 等价wn.call(person2)
显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数
没有this的作用域，所以显式调用没有用

wn（）显式绑定无效，外层的函数存在this，并且这个this
隐式绑定了 person1，所以上层作用域 - person1 ^rnHmBdq3

等价于
foo4: function () {
    return wn
} ^SZQUba72


# Embedded files
2f3022bcc73c3dbecbe68ab68d57d45a8bcf4cb0: [[Pasted Image 20241031220629_384.png]]

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.10",
	"elements": [
		{
			"id": "BtYklQRVXmYNlPnjeYK1t",
			"type": "image",
			"x": -149.40854164831023,
			"y": -444.31771087646484,
			"width": 619.232277776962,
			"height": 826.3333740234375,
			"angle": 0,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 749689483,
			"version": 139,
			"versionNonce": 82907179,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "D2g9vJo-NsIv9aFy_6c23",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"status": "pending",
			"fileId": "2f3022bcc73c3dbecbe68ab68d57d45a8bcf4cb0",
			"scale": [
				1,
				1
			]
		},
		{
			"id": "D2g9vJo-NsIv9aFy_6c23",
			"type": "arrow",
			"x": -125.06681054486177,
			"y": 72.62682851155614,
			"width": 106.63278328886346,
			"height": 328.38071701326214,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 686387813,
			"version": 1239,
			"versionNonce": 984874533,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-106.63278328886346,
					-328.38071701326214
				]
			],
			"lastCommittedPoint": null,
			"startBinding": null,
			"endBinding": {
				"elementId": "26YgbynY",
				"focus": -0.20946669960352485,
				"gap": 10.17480463387352
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "_WjmElcXRYT6Cyu24-efK",
			"type": "arrow",
			"x": -124.16660563151095,
			"y": 99.29349517822277,
			"width": 128.63987273973015,
			"height": 275.55558268229163,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 429817995,
			"version": 583,
			"versionNonce": 2033066667,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-128.63987273973015,
					-275.55558268229163
				]
			],
			"lastCommittedPoint": null,
			"startBinding": null,
			"endBinding": {
				"elementId": "y3udzeP1",
				"focus": -0.7236815530164113,
				"gap": 10.777791341145928
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "B89uRXwnXRwoHXfz12mlx",
			"type": "rectangle",
			"x": -120.61110432942758,
			"y": -362.03987884521484,
			"width": 302.22233072916674,
			"height": 68.44445800781256,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1141456971,
			"version": 109,
			"versionNonce": 2018153803,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "uziww2uWBHTKuV1cNO6S6",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"id": "1KiPgV28",
			"type": "text",
			"x": 517.1855544438686,
			"y": -436.55021917183524,
			"width": 66.71875,
			"height": 46,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"Ssyc1IdUXiBUfbeeF5T7F"
			],
			"frameId": null,
			"roundness": null,
			"seed": 662709643,
			"version": 475,
			"versionNonce": 1017160715,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447089714,
			"link": null,
			"locked": false,
			"text": "等价与\nfoo1: fn",
			"rawText": "等价与\nfoo1: fn",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 41,
			"containerId": null,
			"originalText": "等价与\nfoo1: fn",
			"lineHeight": 1.15
		},
		{
			"id": "wkxCDGyzRw5w7JSvNuJg4",
			"type": "rectangle",
			"x": 495.8522211105353,
			"y": -448.10578150907486,
			"width": 109.33333333333337,
			"height": 65.77777099609375,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"Ssyc1IdUXiBUfbeeF5T7F"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 2079504613,
			"version": 496,
			"versionNonce": 547744427,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "uziww2uWBHTKuV1cNO6S6",
					"type": "arrow"
				}
			],
			"updated": 1730447089714,
			"link": null,
			"locked": false
		},
		{
			"id": "uziww2uWBHTKuV1cNO6S6",
			"type": "arrow",
			"x": 190.86197819069358,
			"y": -327.950971558886,
			"width": 294.32357625317513,
			"height": 68.5811050772914,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1078470309,
			"version": 998,
			"versionNonce": 1051032555,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1730447089714,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					294.32357625317513,
					-68.5811050772914
				]
			],
			"lastCommittedPoint": [
				-255.11108398437506,
				-164.4444376627605
			],
			"startBinding": {
				"elementId": "B89uRXwnXRwoHXfz12mlx",
				"focus": 0.5310063857578344,
				"gap": 9.25075179095441
			},
			"endBinding": {
				"elementId": "wkxCDGyzRw5w7JSvNuJg4",
				"focus": -0.07586156724176722,
				"gap": 10.666666666666686
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "krzJO7jCY9kALBFZMc62f",
			"type": "rectangle",
			"x": -126.83327229817758,
			"y": -269.5954208374023,
			"width": 335.11116536458337,
			"height": 118.22224934895831,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 2096794661,
			"version": 118,
			"versionNonce": 1326314795,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "Uof1vl6oZl5Rpn71ASDXF",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"id": "NdxNM3Bm",
			"type": "text",
			"x": 508.7686684301025,
			"y": -351.6728623149613,
			"width": 151.201171875,
			"height": 92,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"8ECzhdvyFjX0UBmn2fDPy"
			],
			"frameId": null,
			"roundness": null,
			"seed": 2005997029,
			"version": 403,
			"versionNonce": 1467744997,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447073647,
			"link": null,
			"locked": false,
			"text": "等价于\nfoo3: function () {\n    return fn\n}",
			"rawText": "等价于\nfoo3: function () {\n    return fn\n}",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 87,
			"containerId": null,
			"originalText": "等价于\nfoo3: function () {\n    return fn\n}",
			"lineHeight": 1.15
		},
		{
			"id": "30dwvJPG17A5RZSoDbbJC",
			"type": "rectangle",
			"x": 495.43533509676905,
			"y": -361.45065365610714,
			"width": 192.0000000000001,
			"height": 112.88891601562506,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"8ECzhdvyFjX0UBmn2fDPy"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1720434757,
			"version": 358,
			"versionNonce": 153378373,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "Uof1vl6oZl5Rpn71ASDXF",
					"type": "arrow"
				}
			],
			"updated": 1730447073647,
			"link": null,
			"locked": false
		},
		{
			"id": "Uof1vl6oZl5Rpn71ASDXF",
			"type": "arrow",
			"x": 217.40159752588022,
			"y": -206.6481417957878,
			"width": 270.9225722063055,
			"height": 106.98122243788356,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 45784363,
			"version": 508,
			"versionNonce": 1225892299,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1730447084238,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					270.9225722063055,
					-106.98122243788356
				]
			],
			"lastCommittedPoint": [
				265.7778320312501,
				-27.55558268229163
			],
			"startBinding": {
				"elementId": "krzJO7jCY9kALBFZMc62f",
				"focus": 0.5875298030666498,
				"gap": 9.123704459474425
			},
			"endBinding": {
				"elementId": "30dwvJPG17A5RZSoDbbJC",
				"focus": 0.5229256580986409,
				"gap": 7.111165364583286
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "26YgbynY",
			"type": "text",
			"x": -402.3890177408859,
			"y": -426.9286931355795,
			"width": 224.51171875,
			"height": 161,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"NicZ7SVaxFVoqvslpcAtF"
			],
			"frameId": null,
			"roundness": null,
			"seed": 552215333,
			"version": 635,
			"versionNonce": 451397925,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "D2g9vJo-NsIv9aFy_6c23",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "等价与 person1的属性\nfoo1里面的\nfunction () {\n    console.log(this.name)\n}\n\nperson1.fool() 等价与 fn()",
			"rawText": "等价与 person1的属性\nfoo1里面的\nfunction () {\n    console.log(this.name)\n}\n\nperson1.fool() 等价与 fn()",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 156,
			"containerId": null,
			"originalText": "等价与 person1的属性\nfoo1里面的\nfunction () {\n    console.log(this.name)\n}\n\nperson1.fool() 等价与 fn()",
			"lineHeight": 1.15
		},
		{
			"id": "w51w1WItWN5RQB4BPL1Y0",
			"type": "rectangle",
			"x": -430.833353678386,
			"y": -437.59542083740234,
			"width": 264.0000000000001,
			"height": 185.77775065104174,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"NicZ7SVaxFVoqvslpcAtF"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 2099812651,
			"version": 220,
			"versionNonce": 1060145067,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"id": "y3udzeP1",
			"type": "text",
			"x": -442.3888549804693,
			"y": -210.0398788452148,
			"width": 203.3984375,
			"height": 23,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"btZKsG3QhkbjckHQpg09j"
			],
			"frameId": null,
			"roundness": null,
			"seed": 488299205,
			"version": 477,
			"versionNonce": 1874680965,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "_WjmElcXRYT6Cyu24-efK",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "等价与 fn.call(person2)",
			"rawText": "等价与 fn.call(person2)",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 18,
			"containerId": null,
			"originalText": "等价与 fn.call(person2)",
			"lineHeight": 1.15
		},
		{
			"id": "4s0TfS6OJF2WRB265hsI2",
			"type": "rectangle",
			"x": -455.7221069335943,
			"y": -216.26208750406886,
			"width": 219.55550130208343,
			"height": 34.66666666666663,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"btZKsG3QhkbjckHQpg09j"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 2069985701,
			"version": 289,
			"versionNonce": 2058902091,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "60RPZFo9WYmE_-q2IYbvu",
			"type": "rectangle",
			"x": -134.83327229817758,
			"y": 205.96016184488957,
			"width": 139.55550130208337,
			"height": 20.444417317708258,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 759010949,
			"version": 81,
			"versionNonce": 1867088869,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "EN1cKidiRCh_xgwAQ5FBl",
					"type": "arrow"
				}
			],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "MTcWp6El",
			"type": "text",
			"x": -463.7221883138027,
			"y": -122.03987884521484,
			"width": 194.482421875,
			"height": 92,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"ZWwuWu49p6Ag1k4Ubg3DO"
			],
			"frameId": null,
			"roundness": null,
			"seed": 309886789,
			"version": 270,
			"versionNonce": 765050693,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "等价与  fn\n有()说明执行了函数，\n但是里面的return了 fn\n所以就等价与 fn",
			"rawText": "等价与  fn\n有()说明执行了函数，\n但是里面的return了 fn\n所以就等价与 fn",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 87,
			"containerId": null,
			"originalText": "等价与  fn\n有()说明执行了函数，\n但是里面的return了 fn\n所以就等价与 fn",
			"lineHeight": 1.15
		},
		{
			"id": "4J09yvfUex2sxm9grEfvI",
			"type": "rectangle",
			"x": -473.4999389648444,
			"y": -131.81771087646473,
			"width": 219.55558268229174,
			"height": 107.55558268229163,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"ZWwuWu49p6Ag1k4Ubg3DO"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 534716389,
			"version": 220,
			"versionNonce": 1633190795,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "EN1cKidiRCh_xgwAQ5FBl",
					"type": "arrow"
				}
			],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "EN1cKidiRCh_xgwAQ5FBl",
			"type": "arrow",
			"x": -96.30463423306409,
			"y": 202.40457916259783,
			"width": 173.75548877071432,
			"height": 214.22229003906267,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1960008299,
			"version": 316,
			"versionNonce": 1628147365,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-173.75548877071432,
					-214.22229003906267
				]
			],
			"lastCommittedPoint": [
				-118.22224934895837,
				-16
			],
			"startBinding": {
				"elementId": "60RPZFo9WYmE_-q2IYbvu",
				"focus": -0.25607559288147913,
				"gap": 3.5555826822917425
			},
			"endBinding": {
				"elementId": "4J09yvfUex2sxm9grEfvI",
				"focus": -0.2604306540699028,
				"gap": 12.444417317708258
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "tR-mWQ06SqebW8_JTd_e_",
			"type": "rectangle",
			"x": -137.46342113092658,
			"y": 200.24863510161885,
			"width": 171.87416972226225,
			"height": 28.27729600798881,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 239878213,
			"version": 174,
			"versionNonce": 407663109,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "YsFtOkFz0p9XCI6gdkf_h",
					"type": "arrow"
				}
			],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "oCtCnq3o",
			"type": "text",
			"x": -411.2777709960943,
			"y": 16.626747131347713,
			"width": 95.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"1JSpwsZ3_p4YpPSrxCMti"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1840703435,
			"version": 170,
			"versionNonce": 913267915,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "等价与 fn()",
			"rawText": "等价与 fn()",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 18,
			"containerId": null,
			"originalText": "等价与 fn()",
			"lineHeight": 1.15
		},
		{
			"id": "kIFZhaR_98rclXbXu9FIu",
			"type": "rectangle",
			"x": -432.61110432942763,
			"y": 3.293413798014342,
			"width": 136.00000000000006,
			"height": 48.000000000000114,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"1JSpwsZ3_p4YpPSrxCMti"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1939640101,
			"version": 196,
			"versionNonce": 811198821,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "YsFtOkFz0p9XCI6gdkf_h",
					"type": "arrow"
				}
			],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "YsFtOkFz0p9XCI6gdkf_h",
			"type": "arrow",
			"x": -141.26425979109626,
			"y": 200.6923767751532,
			"width": 203.17510063103578,
			"height": 137.84346167505547,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1283340261,
			"version": 550,
			"versionNonce": 161450859,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-203.17510063103578,
					-137.84346167505547
				]
			],
			"lastCommittedPoint": [
				-165.33333333333343,
				78.22216796875
			],
			"startBinding": {
				"elementId": "tR-mWQ06SqebW8_JTd_e_",
				"gap": 3.8008386601696884,
				"focus": -0.6512535034229949
			},
			"endBinding": {
				"elementId": "kIFZhaR_98rclXbXu9FIu",
				"gap": 11.555501302083286,
				"focus": 0.3118306972313015
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "7wwQX4l1SHZvzSEeuoxt6",
			"type": "rectangle",
			"x": -135.2195831010797,
			"y": 229.88740201403158,
			"width": 288.1731657555059,
			"height": 17.746736136225877,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1166972613,
			"version": 137,
			"versionNonce": 1880155659,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "ydX6ttVn_3uD9smadX5ru",
					"type": "arrow"
				}
			],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "tQoVVb54",
			"type": "text",
			"x": -448.9174496449664,
			"y": -622.1357272656521,
			"width": 488.669921875,
			"height": 144.12866595267812,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"MnhJvKDDKLrWiaqf1ymgV"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1973417611,
			"version": 571,
			"versionNonce": 1086188715,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "function () {\n    console.log(this.name)\n} \n例如上面等于的匿名函数为fn\n注意不是fn()，有小括号就是执行了这个函数",
			"rawText": "function () {\n    console.log(this.name)\n} \n例如上面等于的匿名函数为fn\n注意不是fn()，有小括号就是执行了这个函数",
			"fontSize": 25.06585494829185,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 138,
			"containerId": null,
			"originalText": "function () {\n    console.log(this.name)\n} \n例如上面等于的匿名函数为fn\n注意不是fn()，有小括号就是执行了这个函数",
			"lineHeight": 1.15
		},
		{
			"id": "2bbs8AgJScrIApVK9mzOT",
			"type": "rectangle",
			"x": -469.43380876115987,
			"y": -632.2881161155372,
			"width": 525.1061177712318,
			"height": 166.2165027049317,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"MnhJvKDDKLrWiaqf1ymgV"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1345438469,
			"version": 421,
			"versionNonce": 602195845,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "rgRLipi8",
			"type": "text",
			"x": -720.4280235994529,
			"y": 104.23085462296552,
			"width": 403.560255655784,
			"height": 258.8220387504772,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"MeEcrmIL8ldKdLnxncpgp"
			],
			"frameId": null,
			"roundness": null,
			"seed": 797845029,
			"version": 918,
			"versionNonce": 1767373925,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445751402,
			"link": null,
			"locked": false,
			"text": "person1.foo3.call(person2) 表示打印的话\nfoo3: function () {\n    console.log (this)// person2\n    return fn\n}\n调用了foo3方法，return得到 fn\n函数内部存在this，call 显式绑定了person2\n\nperson.foo3.call(person2)()\n这个表示的就是fn(),执行了foo3属性的方法，\n返回了fn，后面()在执行返回的函数就是fn()",
			"rawText": "person1.foo3.call(person2) 表示打印的话\nfoo3: function () {\n    console.log (this)// person2\n    return fn\n}\n调用了foo3方法，return得到 fn\n函数内部存在this，call 显式绑定了person2\n\nperson.foo3.call(person2)()\n这个表示的就是fn(),执行了foo3属性的方法，\n返回了fn，后面()在执行返回的函数就是fn()",
			"fontSize": 20.460240217429025,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 253.00000000000006,
			"containerId": null,
			"originalText": "person1.foo3.call(person2) 表示打印的话\nfoo3: function () {\n    console.log (this)// person2\n    return fn\n}\n调用了foo3方法，return得到 fn\n函数内部存在this，call 显式绑定了person2\n\nperson.foo3.call(person2)()\n这个表示的就是fn(),执行了foo3属性的方法，\n返回了fn，后面()在执行返回的函数就是fn()",
			"lineHeight": 1.15
		},
		{
			"id": "7-DXTKXBcdRVP4_C59CAb",
			"type": "rectangle",
			"x": -731.6669364054083,
			"y": 98.17910037838953,
			"width": 418.44305551245196,
			"height": 274.7821004034817,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"MeEcrmIL8ldKdLnxncpgp"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1754310219,
			"version": 414,
			"versionNonce": 1651807845,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "ydX6ttVn_3uD9smadX5ru",
					"type": "arrow"
				}
			],
			"updated": 1730445755965,
			"link": null,
			"locked": false
		},
		{
			"id": "ydX6ttVn_3uD9smadX5ru",
			"type": "arrow",
			"x": -136.90987739676962,
			"y": 237.75717138120223,
			"width": 175.31400349618661,
			"height": 2.2611353095396964,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 504521003,
			"version": 515,
			"versionNonce": 1165230373,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445755965,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-175.31400349618661,
					2.2611353095396964
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "7wwQX4l1SHZvzSEeuoxt6",
				"gap": 1.6902942956899096,
				"focus": 0.26907324600143895
			},
			"endBinding": {
				"elementId": "7-DXTKXBcdRVP4_C59CAb",
				"gap": 1,
				"focus": 0.05110672218905237
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "Vtmxo5pn",
			"type": "text",
			"x": 185.91180690741714,
			"y": 227.35213465216407,
			"width": 80,
			"height": 23,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1203824075,
			"version": 45,
			"versionNonce": 1615071371,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "默认绑定",
			"rawText": "默认绑定",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 18,
			"containerId": null,
			"originalText": "默认绑定",
			"lineHeight": 1.15
		},
		{
			"id": "zmBpqFTBqd0Hs8BkVCYD9",
			"type": "rectangle",
			"x": -138.60001695320034,
			"y": 252.42552844826736,
			"width": 300.00437475940953,
			"height": 18.591767229626612,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 662465163,
			"version": 153,
			"versionNonce": 1011276197,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "A3B5Gubnd-JxP8WxZrwgT",
					"type": "arrow"
				}
			],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "29virnGI",
			"type": "text",
			"x": -415.1503424401172,
			"y": 412.29470031167716,
			"width": 416.6796875,
			"height": 138,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"Y0XyonXR2jphXgb32xrKJ"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1876729317,
			"version": 598,
			"versionNonce": 724894181,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447102094,
			"link": null,
			"locked": false,
			"text": "person1.foo3() 等价与 fn\n执行了foo3的方法，return 了fn\n\nperson1.foo3().call(person2) = fn.call(person2)\n这是一个显示绑定，对返回的fn的一个绑定调用\n所以显式绑定 - person2 ",
			"rawText": "person1.foo3() 等价与 fn\n执行了foo3的方法，return 了fn\n\nperson1.foo3().call(person2) = fn.call(person2)\n这是一个显示绑定，对返回的fn的一个绑定调用\n所以显式绑定 - person2 ",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 133,
			"containerId": null,
			"originalText": "person1.foo3() 等价与 fn\n执行了foo3的方法，return 了fn\n\nperson1.foo3().call(person2) = fn.call(person2)\n这是一个显示绑定，对返回的fn的一个绑定调用\n所以显式绑定 - person2 ",
			"lineHeight": 1.15
		},
		{
			"id": "D2m8Vd-ijkTYrHXmb9hcZ",
			"type": "rectangle",
			"x": -425.46176577892305,
			"y": 413.1422690424912,
			"width": 454.03221565230183,
			"height": 145.88315569596773,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"Y0XyonXR2jphXgb32xrKJ"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 245504587,
			"version": 362,
			"versionNonce": 459636037,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "A3B5Gubnd-JxP8WxZrwgT",
					"type": "arrow"
				}
			],
			"updated": 1730447102094,
			"link": null,
			"locked": false
		},
		{
			"id": "A3B5Gubnd-JxP8WxZrwgT",
			"type": "arrow",
			"x": -117.07229831619259,
			"y": 274.52970030573385,
			"width": 208.5498889503732,
			"height": 133.9318242454965,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1449738405,
			"version": 506,
			"versionNonce": 2025893893,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447102094,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-208.5498889503732,
					133.9318242454965
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "zmBpqFTBqd0Hs8BkVCYD9",
				"focus": 0.6592656774180405,
				"gap": 3.512404627839885
			},
			"endBinding": {
				"elementId": "D2m8Vd-ijkTYrHXmb9hcZ",
				"focus": -0.7282673976568774,
				"gap": 4.680744491260839
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "0XWBjr2t0tOKh8ztlyjD3",
			"type": "rectangle",
			"x": -131.2788983672059,
			"y": 300.1435461767681,
			"width": 135.74159024656456,
			"height": 17.162682186294546,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 630472331,
			"version": 94,
			"versionNonce": 662598757,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "oLnRem64",
			"type": "text",
			"x": 107.78854370564315,
			"y": -622.8997479887881,
			"width": 452.6298026417609,
			"height": 137.38255982033547,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"lXlmcFLLxw1-G4HBDDxgv"
			],
			"frameId": null,
			"roundness": null,
			"seed": 2143245515,
			"version": 155,
			"versionNonce": 1049750283,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "() => {\n    console.log(this.name)\n}\n例如上面的箭头函数为wn\n注意不是wn()，有小括号就是执行了这个函",
			"rawText": "() => {\n    console.log(this.name)\n}\n例如上面的箭头函数为wn\n注意不是wn()，有小括号就是执行了这个函",
			"fontSize": 23.892619099188778,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 132,
			"containerId": null,
			"originalText": "() => {\n    console.log(this.name)\n}\n例如上面的箭头函数为wn\n注意不是wn()，有小括号就是执行了这个函",
			"lineHeight": 1.15
		},
		{
			"id": "nCmYZAzV8pvSKDdiuMUHq",
			"type": "rectangle",
			"x": 81.78991254462949,
			"y": -637.5945960994247,
			"width": 525.6231047123038,
			"height": 168.42548520968893,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"lXlmcFLLxw1-G4HBDDxgv"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1069897221,
			"version": 136,
			"versionNonce": 471752485,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "85W6Jx7BNiqvzx_NvSAHG",
			"type": "arrow",
			"x": -23.239531684836265,
			"y": 305.7772736448439,
			"width": 498.326478567334,
			"height": 340.62122810085714,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 2024307461,
			"version": 732,
			"versionNonce": 1863724293,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447004788,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					498.326478567334,
					-340.62122810085714
				]
			],
			"lastCommittedPoint": null,
			"startBinding": null,
			"endBinding": {
				"elementId": "SHUuSF6M",
				"focus": 0.852550882089212,
				"gap": 3.9387586996857635
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "SHUuSF6M",
			"type": "text",
			"x": 479.0257055821835,
			"y": -50.87885615986312,
			"width": 231.123046875,
			"height": 23,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"-nmUJWVw0BSQGVBGsI6XN"
			],
			"frameId": null,
			"roundness": null,
			"seed": 804867787,
			"version": 738,
			"versionNonce": 623946149,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "85W6Jx7BNiqvzx_NvSAHG",
					"type": "arrow"
				}
			],
			"updated": 1730447004788,
			"link": null,
			"locked": false,
			"text": "等价于放回的箭头函数 wn",
			"rawText": "等价于放回的箭头函数 wn",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 18,
			"containerId": null,
			"originalText": "等价于放回的箭头函数 wn",
			"lineHeight": 1.15
		},
		{
			"id": "nbrBLIGSMw8g8ZlxFrFEd",
			"type": "rectangle",
			"x": 473.19446827271497,
			"y": -70.79139349396456,
			"width": 259.2617730065447,
			"height": 58.665017712070494,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"-nmUJWVw0BSQGVBGsI6XN"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 250701733,
			"version": 690,
			"versionNonce": 473187429,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447004788,
			"link": null,
			"locked": false
		},
		{
			"id": "KyyDK-ytD_PwK6a-KUbFx",
			"type": "rectangle",
			"x": -133.64288159089298,
			"y": 295.6698036352478,
			"width": 178.09882120667496,
			"height": 23.567970320086204,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1970488971,
			"version": 174,
			"versionNonce": 1089869995,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445406250,
			"link": null,
			"locked": false
		},
		{
			"id": "hdsyD5jr",
			"type": "text",
			"x": 485.21314767345825,
			"y": 18.42417450972357,
			"width": 104.443359375,
			"height": 23,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"y-UPCbc786RDXEr8MFfZG"
			],
			"frameId": null,
			"roundness": null,
			"seed": 799263563,
			"version": 309,
			"versionNonce": 960715813,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447002607,
			"link": null,
			"locked": false,
			"text": "等价于 wn()",
			"rawText": "等价于 wn()",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 18,
			"containerId": null,
			"originalText": "等价于 wn()",
			"lineHeight": 1.15
		},
		{
			"id": "9sc4RWpOrl8SRYA_0j2TT",
			"type": "rectangle",
			"x": 479.33853239101154,
			"y": 8.353317643197556,
			"width": 129.24261189739013,
			"height": 40.28342746610406,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"y-UPCbc786RDXEr8MFfZG"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 195284645,
			"version": 331,
			"versionNonce": 53383045,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "OgOuhmCeMYHCxIFOcwSGF",
					"type": "arrow"
				}
			],
			"updated": 1730447002607,
			"link": null,
			"locked": false
		},
		{
			"id": "OgOuhmCeMYHCxIFOcwSGF",
			"type": "arrow",
			"x": 42.579287766751236,
			"y": 299.9925580802651,
			"width": 435.1609420957412,
			"height": 250.84309165231076,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1158293157,
			"version": 397,
			"versionNonce": 68966117,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447002607,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					435.1609420957412,
					-250.84309165231076
				]
			],
			"lastCommittedPoint": null,
			"startBinding": null,
			"endBinding": {
				"elementId": "9sc4RWpOrl8SRYA_0j2TT",
				"focus": 0.30521805423673165,
				"gap": 1.6785273674479413
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "yMgWJKxr2jLDr9aQeiqmQ",
			"type": "rectangle",
			"x": -132.65182196572482,
			"y": 319.89833179615295,
			"width": 311.90719720378195,
			"height": 25.13106856044709,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 788493515,
			"version": 187,
			"versionNonce": 1403613451,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730445489424,
			"link": null,
			"locked": false
		},
		{
			"id": "xgbC6oiJ",
			"type": "text",
			"x": 519.047100296532,
			"y": 72.59714758068435,
			"width": 456.689453125,
			"height": 276,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"z38JZOthW4vPK0bm_v01p"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1460475819,
			"version": 503,
			"versionNonce": 511814085,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730446991903,
			"link": null,
			"locked": false,
			"text": "person1.foo4.call(person2) 表示打印的话\nfoo4: funtion () {\n    console.log(this) //person2\n    reurn wn\n}\n调用了foo4方法，return得到wn\n函数内部存在this，call 显式绑定了person2\n\nperson1.foo4.call(person2)() 等价与 wn()\n\nwn是一个箭头函数里面this作用域，向外找到外层的\n函数内部显式绑定的 person2",
			"rawText": "person1.foo4.call(person2) 表示打印的话\nfoo4: funtion () {\n    console.log(this) //person2\n    reurn wn\n}\n调用了foo4方法，return得到wn\n函数内部存在this，call 显式绑定了person2\n\nperson1.foo4.call(person2)() 等价与 wn()\n\nwn是一个箭头函数里面this作用域，向外找到外层的\n函数内部显式绑定的 person2",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 271,
			"containerId": null,
			"originalText": "person1.foo4.call(person2) 表示打印的话\nfoo4: funtion () {\n    console.log(this) //person2\n    reurn wn\n}\n调用了foo4方法，return得到wn\n函数内部存在this，call 显式绑定了person2\n\nperson1.foo4.call(person2)() 等价与 wn()\n\nwn是一个箭头函数里面this作用域，向外找到外层的\n函数内部显式绑定的 person2",
			"lineHeight": 1.15
		},
		{
			"id": "t2KZFdx-dL5qk5Y0_nJDI",
			"type": "rectangle",
			"x": 497.16376067628084,
			"y": 61.995509051558486,
			"width": 503.30381590772686,
			"height": 289.52318721222827,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"z38JZOthW4vPK0bm_v01p"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 64968235,
			"version": 151,
			"versionNonce": 1922181413,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "tm1Q5CGILFJciijvyY_XD",
					"type": "arrow"
				}
			],
			"updated": 1730446991903,
			"link": null,
			"locked": false
		},
		{
			"id": "tm1Q5CGILFJciijvyY_XD",
			"type": "arrow",
			"x": 177.80988495304985,
			"y": 323.7368168258515,
			"width": 318.353875723231,
			"height": 94.67229944805587,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 615928747,
			"version": 146,
			"versionNonce": 589020293,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730446991903,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					318.353875723231,
					-94.67229944805587
				]
			],
			"lastCommittedPoint": null,
			"startBinding": null,
			"endBinding": {
				"elementId": "t2KZFdx-dL5qk5Y0_nJDI",
				"gap": 1,
				"focus": 0.24055949392036993
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "NDoBOJLpWEeHYXrnjeUut",
			"type": "rectangle",
			"x": -135.8031215829471,
			"y": 346.35467217424514,
			"width": 314.9665523146823,
			"height": 26.591076632122167,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1180429253,
			"version": 116,
			"versionNonce": 1432483883,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "vic2k3yylI6UsoVoEw_KZ",
					"type": "arrow"
				}
			],
			"updated": 1730446970533,
			"link": null,
			"locked": false
		},
		{
			"id": "rnHmBdq3",
			"type": "text",
			"x": 226.16159324504815,
			"y": 382.6720212772146,
			"width": 513.427734375,
			"height": 207,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"ux-FA54TzR2_fZHBQg5UO"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1103953893,
			"version": 826,
			"versionNonce": 277330283,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "vic2k3yylI6UsoVoEw_KZ",
					"type": "arrow"
				}
			],
			"updated": 1730446976224,
			"link": null,
			"locked": false,
			"text": "person1.foo4()等价于 wn\n() 说明调用了foo4的方法 ，通过return返回了 wn\n\nperson1.foo4().call(person2) 等价wn.call(person2)\n显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数\n没有this的作用域，所以显式调用没有用\n\nwn（）显式绑定无效，外层的函数存在this，并且这个this\n隐式绑定了 person1，所以上层作用域 - person1",
			"rawText": "person1.foo4()等价于 wn\n() 说明调用了foo4的方法 ，通过return返回了 wn\n\nperson1.foo4().call(person2) 等价wn.call(person2)\n显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数\n没有this的作用域，所以显式调用没有用\n\nwn（）显式绑定无效，外层的函数存在this，并且这个this\n隐式绑定了 person1，所以上层作用域 - person1",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 202,
			"containerId": null,
			"originalText": "person1.foo4()等价于 wn\n() 说明调用了foo4的方法 ，通过return返回了 wn\n\nperson1.foo4().call(person2) 等价wn.call(person2)\n显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数\n没有this的作用域，所以显式调用没有用\n\nwn（）显式绑定无效，外层的函数存在this，并且这个this\n隐式绑定了 person1，所以上层作用域 - person1",
			"lineHeight": 1.15
		},
		{
			"id": "PB11YUXrZrjsJL8HkjiVg",
			"type": "rectangle",
			"x": 212.06650153228452,
			"y": 382.6720212772143,
			"width": 546.401943979285,
			"height": 211.43017118367857,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"ux-FA54TzR2_fZHBQg5UO"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 208515301,
			"version": 326,
			"versionNonce": 1908411723,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730446976225,
			"link": null,
			"locked": false
		},
		{
			"id": "vic2k3yylI6UsoVoEw_KZ",
			"type": "arrow",
			"x": 180.71739422924117,
			"y": 374.5922707249743,
			"width": 41.298610597880554,
			"height": 21.070619031876845,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 154104581,
			"version": 346,
			"versionNonce": 301111979,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1730446976225,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					41.298610597880554,
					21.070619031876845
				]
			],
			"lastCommittedPoint": [
				69.64758580168234,
				38.14029399912033
			],
			"startBinding": {
				"elementId": "NDoBOJLpWEeHYXrnjeUut",
				"focus": -0.7132215078496554,
				"gap": 2.264031134952461
			},
			"endBinding": {
				"elementId": "rnHmBdq3",
				"focus": -0.18160417791800604,
				"gap": 4.145588417926433
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "Wj4Y7OOnzsxxPK4gIm6jI",
			"type": "rectangle",
			"x": -138.16473813297983,
			"y": -154.8433619761983,
			"width": 367.30807600797186,
			"height": 139.29520955828679,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1931051435,
			"version": 179,
			"versionNonce": 1887322859,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "2unM3VXMMNOMp0Q7jqIPE",
					"type": "arrow"
				}
			],
			"updated": 1730447068772,
			"link": null,
			"locked": false
		},
		{
			"id": "SZQUba72",
			"type": "text",
			"x": 502.7589294343028,
			"y": -202.93334904476694,
			"width": 151.201171875,
			"height": 92,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"e4gFd0-HoCZ9xQU-Iom0B"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1836723083,
			"version": 134,
			"versionNonce": 86106117,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "2unM3VXMMNOMp0Q7jqIPE",
					"type": "arrow"
				}
			],
			"updated": 1730447072259,
			"link": null,
			"locked": false,
			"text": "等价于\nfoo4: function () {\n    return wn\n}",
			"rawText": "等价于\nfoo4: function () {\n    return wn\n}",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 87,
			"containerId": null,
			"originalText": "等价于\nfoo4: function () {\n    return wn\n}",
			"lineHeight": 1.15
		},
		{
			"id": "FpXk_W5CrSd9jrgpuFgzt",
			"type": "rectangle",
			"x": 481.20129274626674,
			"y": -216.1995432124943,
			"width": 204.7971689871202,
			"height": 114.4210717719717,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"e4gFd0-HoCZ9xQU-Iom0B"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 815561157,
			"version": 146,
			"versionNonce": 985973285,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447072260,
			"link": null,
			"locked": false
		},
		{
			"id": "2unM3VXMMNOMp0Q7jqIPE",
			"type": "arrow",
			"x": 230.80158842413158,
			"y": -65.83631559502582,
			"width": 256.20369510889014,
			"height": 84.55772032129268,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 309087717,
			"version": 190,
			"versionNonce": 391340741,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1730447072260,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					256.20369510889014,
					-84.55772032129268
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "Wj4Y7OOnzsxxPK4gIm6jI",
				"focus": 0.6191264901131911,
				"gap": 1.6582505491395523
			},
			"endBinding": {
				"elementId": "SZQUba72",
				"focus": 0.33278220912403245,
				"gap": 15.753645901281061
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "yLKNTK_1lEm3rnwKP_d_M",
			"type": "rectangle",
			"x": -137.50002034505246,
			"y": 55.7378718058269,
			"width": 116.44441731770837,
			"height": 21.333333333333258,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 418858347,
			"version": 93,
			"versionNonce": 1250401285,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"id": "PgzSKNE0cAQcG0lMk4jPH",
			"type": "rectangle",
			"x": -134.83335367838583,
			"y": 60.18237050374353,
			"width": 120.00000000000011,
			"height": 20.44441731770837,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1645881835,
			"version": 98,
			"versionNonce": 945017547,
			"isDeleted": true,
			"boundElements": [
				{
					"id": "D2g9vJo-NsIv9aFy_6c23",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"id": "GPHpQLUi8-HC-U_JW-lmq",
			"type": "rectangle",
			"x": -590.8333536783858,
			"y": -524.7065658569336,
			"width": 270.2222493489585,
			"height": 188.44443766276046,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1018672837,
			"version": 406,
			"versionNonce": 94360421,
			"isDeleted": true,
			"boundElements": [
				{
					"id": "D2g9vJo-NsIv9aFy_6c23",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"id": "8B7VeburseiQzpCLAZCc4",
			"type": "arrow",
			"x": -134.83335367838583,
			"y": 54.32375988498896,
			"width": 186.02392029465898,
			"height": 404.5370571466542,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 576221835,
			"version": 439,
			"versionNonce": 59064683,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-186.02392029465898,
					-404.5370571466542
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "PgzSKNE0cAQcG0lMk4jPH",
				"focus": -0.8130576146902633,
				"gap": 5.858610618754568
			},
			"endBinding": {
				"elementId": "26YgbynY",
				"focus": -0.6155768678176825,
				"gap": 12.605881137632764
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "jcLG_APLVblCRmguzpsOr",
			"type": "arrow",
			"x": -92.16676839192758,
			"y": 77.07375587435592,
			"width": 241.4472949452599,
			"height": 456.2343676605276,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 148414181,
			"version": 579,
			"versionNonce": 1400512197,
			"isDeleted": true,
			"boundElements": [],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-72.00008138020826,
					-130.4054136811372
				],
				[
					-241.4472949452599,
					-456.2343676605276
				]
			],
			"lastCommittedPoint": [
				-205.33333333333337,
				-397.3333740234376
			],
			"startBinding": null,
			"endBinding": {
				"elementId": "26YgbynY",
				"focus": -0.6242122962867251,
				"gap": 13.152070289115102
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "p9O1uL3s",
			"type": "text",
			"x": -189.16733805338583,
			"y": -72.83169849688541,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 99445931,
			"version": 12,
			"versionNonce": 1339022347,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "jcLG_APLVblCRmguzpsOr",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "ZwJhYa-tHLSt0-L0WpuWB",
			"type": "arrow",
			"x": -572.1666056315111,
			"y": -250.9287541707356,
			"width": 51.55550130208337,
			"height": 24.888875325520814,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1379205509,
			"version": 40,
			"versionNonce": 305852805,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					51.55550130208337,
					24.888875325520814
				]
			],
			"lastCommittedPoint": [
				51.55550130208337,
				24.888875325520814
			],
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "O9IkjrO0",
			"type": "text",
			"x": 529.4997355143225,
			"y": -362.87326304117846,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"Ssyc1IdUXiBUfbeeF5T7F"
			],
			"frameId": null,
			"roundness": null,
			"seed": 602378021,
			"version": 9,
			"versionNonce": 58070085,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "wkxCDGyzRw5w7JSvNuJg4",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "TRL2Z8by",
			"type": "text",
			"x": -252.72271728515685,
			"y": -454.8732223510742,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 471052357,
			"version": 12,
			"versionNonce": 1117078437,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "uziww2uWBHTKuV1cNO6S6",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "63n-RKmvn-oecC57RfvS3",
			"type": "arrow",
			"x": -136.61110432942758,
			"y": -244.7065353393554,
			"width": 188.44441731770843,
			"height": 88,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 763977861,
			"version": 132,
			"versionNonce": 1220173413,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-188.44441731770843,
					-88
				]
			],
			"lastCommittedPoint": [
				-188.44441731770843,
				-88
			],
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "aGAnnyzN",
			"type": "text",
			"x": -323.8180449455843,
			"y": -304.15198386084535,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1418306949,
			"version": 9,
			"versionNonce": 2104288875,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "63n-RKmvn-oecC57RfvS3",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "KaV9GiE3",
			"type": "text",
			"x": 345.4994913736976,
			"y": -285.98429616292304,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 510774923,
			"version": 9,
			"versionNonce": 1467670795,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "Uof1vl6oZl5Rpn71ASDXF",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "loRCV4TQgK1-OYmWKoUsj",
			"type": "line",
			"x": -484.16660563151106,
			"y": 192.6268285115562,
			"width": 13.333333333333371,
			"height": 16,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 177135845,
			"version": 80,
			"versionNonce": 653056235,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					13.333333333333371,
					16
				]
			],
			"lastCommittedPoint": [
				13.333333333333371,
				16
			],
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": null
		},
		{
			"id": "08JYlKNF",
			"type": "text",
			"x": -200.2782999674485,
			"y": 191.79349517822283,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 699802763,
			"version": 9,
			"versionNonce": 842390059,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "EN1cKidiRCh_xgwAQ5FBl",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "PYktqsfD",
			"type": "text",
			"x": -238.0560913085943,
			"y": 254.90457916259783,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1639561637,
			"version": 9,
			"versionNonce": 176256197,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "YsFtOkFz0p9XCI6gdkf_h",
			"originalText": "",
			"lineHeight": 1.15
		},
		{
			"id": "po0AMSp8zpcLqkz1xka0_",
			"type": "rectangle",
			"x": -201.9811400700919,
			"y": -700.5486984977267,
			"width": 197.7493455179458,
			"height": 185.91819454126426,
			"angle": 0,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 605154347,
			"version": 57,
			"versionNonce": 39883813,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"id": "1VfbTki-rA1IYYDPzbzuv",
			"type": "rectangle",
			"x": -602.5504045145346,
			"y": 164.81596525904365,
			"width": 296.62401827691866,
			"height": 141.12885799640662,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 919575947,
			"version": 59,
			"versionNonce": 256974667,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"text": "function () {\r\n    console.log(this.name)\r\n} \r\n例如上面等于的匿名函数为fn\r\n注意不是fn()，有小括号就是执行了这个函数",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 110,
			"id": "3DLkIgaR",
			"type": "text",
			"x": -415.9168885297624,
			"y": -498.0285434074015,
			"width": 390,
			"height": 115,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"roundness": null,
			"seed": 13474,
			"version": 4,
			"versionNonce": 1658625989,
			"updated": 1730445375872,
			"isDeleted": true,
			"groupIds": [],
			"boundElements": [],
			"link": null,
			"locked": false,
			"containerId": null,
			"originalText": "function () {\r\n    console.log(this.name)\r\n} \r\n例如上面等于的匿名函数为fn\r\n注意不是fn()，有小括号就是执行了这个函数",
			"rawText": "function () {\r\n    console.log(this.name)\r\n} \r\n例如上面等于的匿名函数为fn\r\n注意不是fn()，有小括号就是执行了这个函数",
			"lineHeight": 1.15
		},
		{
			"id": "MJat-zFKS6N_-ffxA8osZ",
			"type": "arrow",
			"x": -3.369112679182308,
			"y": 300.1000110717999,
			"width": 203.43521332469209,
			"height": 91.7824404735951,
			"angle": 0,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 590539307,
			"version": 60,
			"versionNonce": 47600043,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					203.43521332469209,
					-91.7824404735951
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "0XWBjr2t0tOKh8ztlyjD3",
				"focus": 0.47095638855882493,
				"gap": 1
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "ONb0sa0K",
			"type": "text",
			"x": 211.77544317872724,
			"y": 382.77992694087993,
			"width": 5.556640625,
			"height": 23,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 975210885,
			"version": 2,
			"versionNonce": 1914101035,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1730446971178,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 2,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 18,
			"containerId": "vic2k3yylI6UsoVoEw_KZ",
			"originalText": "",
			"lineHeight": 1.15
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
		"scrollX": 659.6926202357944,
		"scrollY": 841.8230597771864,
		"zoom": {
			"value": 0.8040479702980217
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