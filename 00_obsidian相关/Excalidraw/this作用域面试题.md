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
			"type": "image",
			"version": 139,
			"versionNonce": 82907179,
			"isDeleted": false,
			"id": "BtYklQRVXmYNlPnjeYK1t",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -149.40854164831023,
			"y": -444.31771087646484,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"width": 619.232277776962,
			"height": 826.3333740234375,
			"seed": 749689483,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
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
			"type": "arrow",
			"version": 1239,
			"versionNonce": 984874533,
			"isDeleted": false,
			"id": "D2g9vJo-NsIv9aFy_6c23",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -125.06681054486177,
			"y": 72.62682851155614,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 106.63278328886346,
			"height": 328.38071701326214,
			"seed": 686387813,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": {
				"elementId": "26YgbynY",
				"focus": -0.20946669960352485,
				"gap": 10.17480463387352
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-106.63278328886346,
					-328.38071701326214
				]
			]
		},
		{
			"type": "arrow",
			"version": 583,
			"versionNonce": 2033066667,
			"isDeleted": false,
			"id": "_WjmElcXRYT6Cyu24-efK",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -124.16660563151095,
			"y": 99.29349517822277,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 128.63987273973015,
			"height": 275.55558268229163,
			"seed": 429817995,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": {
				"elementId": "y3udzeP1",
				"focus": -0.7236815530164113,
				"gap": 10.777791341145928
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-128.63987273973015,
					-275.55558268229163
				]
			]
		},
		{
			"type": "rectangle",
			"version": 109,
			"versionNonce": 2018153803,
			"isDeleted": false,
			"id": "B89uRXwnXRwoHXfz12mlx",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -120.61110432942758,
			"y": -362.03987884521484,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 302.22233072916674,
			"height": 68.44445800781256,
			"seed": 1141456971,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 491,
			"versionNonce": 940832964,
			"isDeleted": false,
			"id": "1KiPgV28",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 763.6366652837123,
			"y": -814.1498590644134,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 68.5799560546875,
			"height": 46,
			"seed": 662709643,
			"groupIds": [
				"Ssyc1IdUXiBUfbeeF5T7F"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1749007769336,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价与\nfoo1: fn",
			"rawText": "等价与\nfoo1: fn",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价与\nfoo1: fn",
			"lineHeight": 1.15,
			"baseline": 41
		},
		{
			"type": "rectangle",
			"version": 512,
			"versionNonce": 1478508612,
			"isDeleted": false,
			"id": "wkxCDGyzRw5w7JSvNuJg4",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 742.3033319503791,
			"y": -825.705421401653,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 109.33333333333337,
			"height": 65.77777099609375,
			"seed": 2079504613,
			"groupIds": [
				"Ssyc1IdUXiBUfbeeF5T7F"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [
				{
					"id": "uziww2uWBHTKuV1cNO6S6",
					"type": "arrow"
				}
			],
			"updated": 1749007769336,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 1034,
			"versionNonce": 1663827524,
			"isDeleted": false,
			"id": "uziww2uWBHTKuV1cNO6S6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 190.35039275158454,
			"y": -365.07358617661976,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 551.7947558556194,
			"height": 384.18857053161264,
			"seed": 1078470309,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1749007769464,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					551.7947558556194,
					-384.18857053161264
				]
			]
		},
		{
			"type": "rectangle",
			"version": 118,
			"versionNonce": 1326314795,
			"isDeleted": false,
			"id": "krzJO7jCY9kALBFZMc62f",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -126.83327229817758,
			"y": -269.5954208374023,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 335.11116536458337,
			"height": 118.22224934895831,
			"seed": 2096794661,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 403,
			"versionNonce": 1467744997,
			"isDeleted": false,
			"id": "NdxNM3Bm",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 508.7686684301025,
			"y": -351.6728623149613,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 159.5198516845703,
			"height": 92,
			"seed": 2005997029,
			"groupIds": [
				"8ECzhdvyFjX0UBmn2fDPy"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730447073647,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价于\nfoo3: function () {\n    return fn\n}",
			"rawText": "等价于\nfoo3: function () {\n    return fn\n}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价于\nfoo3: function () {\n    return fn\n}",
			"lineHeight": 1.15,
			"baseline": 87
		},
		{
			"type": "rectangle",
			"version": 358,
			"versionNonce": 153378373,
			"isDeleted": false,
			"id": "30dwvJPG17A5RZSoDbbJC",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 495.43533509676905,
			"y": -361.45065365610714,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 192.0000000000001,
			"height": 112.88891601562506,
			"seed": 1720434757,
			"groupIds": [
				"8ECzhdvyFjX0UBmn2fDPy"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 508,
			"versionNonce": 1225892299,
			"isDeleted": false,
			"id": "Uof1vl6oZl5Rpn71ASDXF",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 217.40159752588022,
			"y": -206.6481417957878,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 270.9225722063055,
			"height": 106.98122243788356,
			"seed": 45784363,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730447084238,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					270.9225722063055,
					-106.98122243788356
				]
			]
		},
		{
			"type": "text",
			"version": 635,
			"versionNonce": 451397925,
			"isDeleted": false,
			"id": "26YgbynY",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -402.3890177408859,
			"y": -426.9286931355795,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 230.53973388671875,
			"height": 161,
			"seed": 552215333,
			"groupIds": [
				"NicZ7SVaxFVoqvslpcAtF"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "D2g9vJo-NsIv9aFy_6c23",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价与 person1的属性\nfoo1里面的\nfunction () {\n    console.log(this.name)\n}\n\nperson1.fool() 等价与 fn()",
			"rawText": "等价与 person1的属性\nfoo1里面的\nfunction () {\n    console.log(this.name)\n}\n\nperson1.fool() 等价与 fn()",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价与 person1的属性\nfoo1里面的\nfunction () {\n    console.log(this.name)\n}\n\nperson1.fool() 等价与 fn()",
			"lineHeight": 1.15,
			"baseline": 156
		},
		{
			"type": "rectangle",
			"version": 220,
			"versionNonce": 1060145067,
			"isDeleted": false,
			"id": "w51w1WItWN5RQB4BPL1Y0",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -430.833353678386,
			"y": -437.59542083740234,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 264.0000000000001,
			"height": 185.77775065104174,
			"seed": 2099812651,
			"groupIds": [
				"NicZ7SVaxFVoqvslpcAtF"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445375871,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 477,
			"versionNonce": 1874680965,
			"isDeleted": false,
			"id": "y3udzeP1",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -442.3888549804693,
			"y": -210.0398788452148,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 206.81979370117188,
			"height": 23,
			"seed": 488299205,
			"groupIds": [
				"btZKsG3QhkbjckHQpg09j"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "_WjmElcXRYT6Cyu24-efK",
					"type": "arrow"
				}
			],
			"updated": 1730445375871,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价与 fn.call(person2)",
			"rawText": "等价与 fn.call(person2)",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价与 fn.call(person2)",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 289,
			"versionNonce": 2058902091,
			"isDeleted": false,
			"id": "4s0TfS6OJF2WRB265hsI2",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -455.7221069335943,
			"y": -216.26208750406886,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 219.55550130208343,
			"height": 34.66666666666663,
			"seed": 2069985701,
			"groupIds": [
				"btZKsG3QhkbjckHQpg09j"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 81,
			"versionNonce": 1867088869,
			"isDeleted": false,
			"id": "60RPZFo9WYmE_-q2IYbvu",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -134.83327229817758,
			"y": 205.96016184488957,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 139.55550130208337,
			"height": 20.444417317708258,
			"seed": 759010949,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 270,
			"versionNonce": 765050693,
			"isDeleted": false,
			"id": "MTcWp6El",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -463.7221883138027,
			"y": -122.03987884521484,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 200.95980834960938,
			"height": 92,
			"seed": 309886789,
			"groupIds": [
				"ZWwuWu49p6Ag1k4Ubg3DO"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价与  fn\n有()说明执行了函数，\n但是里面的return了 fn\n所以就等价与 fn",
			"rawText": "等价与  fn\n有()说明执行了函数，\n但是里面的return了 fn\n所以就等价与 fn",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价与  fn\n有()说明执行了函数，\n但是里面的return了 fn\n所以就等价与 fn",
			"lineHeight": 1.15,
			"baseline": 87
		},
		{
			"type": "rectangle",
			"version": 220,
			"versionNonce": 1633190795,
			"isDeleted": false,
			"id": "4J09yvfUex2sxm9grEfvI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -473.4999389648444,
			"y": -131.81771087646473,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 219.55558268229174,
			"height": 107.55558268229163,
			"seed": 534716389,
			"groupIds": [
				"ZWwuWu49p6Ag1k4Ubg3DO"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 316,
			"versionNonce": 1628147365,
			"isDeleted": false,
			"id": "EN1cKidiRCh_xgwAQ5FBl",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -96.30463423306409,
			"y": 202.40457916259783,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 173.75548877071432,
			"height": 214.22229003906267,
			"seed": 1960008299,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-173.75548877071432,
					-214.22229003906267
				]
			]
		},
		{
			"type": "rectangle",
			"version": 174,
			"versionNonce": 407663109,
			"isDeleted": false,
			"id": "tR-mWQ06SqebW8_JTd_e_",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -137.46342113092658,
			"y": 200.24863510161885,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 171.87416972226225,
			"height": 28.27729600798881,
			"seed": 239878213,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 170,
			"versionNonce": 913267915,
			"isDeleted": false,
			"id": "oCtCnq3o",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -411.2777709960943,
			"y": 16.626747131347713,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 96.77992248535156,
			"height": 23,
			"seed": 1840703435,
			"groupIds": [
				"1JSpwsZ3_p4YpPSrxCMti"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价与 fn()",
			"rawText": "等价与 fn()",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价与 fn()",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 196,
			"versionNonce": 811198821,
			"isDeleted": false,
			"id": "kIFZhaR_98rclXbXu9FIu",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -432.61110432942763,
			"y": 3.293413798014342,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 136.00000000000006,
			"height": 48.000000000000114,
			"seed": 1939640101,
			"groupIds": [
				"1JSpwsZ3_p4YpPSrxCMti"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 550,
			"versionNonce": 161450859,
			"isDeleted": false,
			"id": "YsFtOkFz0p9XCI6gdkf_h",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -141.26425979109626,
			"y": 200.6923767751532,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 203.17510063103578,
			"height": 137.84346167505547,
			"seed": 1283340261,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-203.17510063103578,
					-137.84346167505547
				]
			]
		},
		{
			"type": "rectangle",
			"version": 137,
			"versionNonce": 1880155659,
			"isDeleted": false,
			"id": "7wwQX4l1SHZvzSEeuoxt6",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -135.2195831010797,
			"y": 229.88740201403158,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 288.1731657555059,
			"height": 17.746736136225877,
			"seed": 1166972613,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 571,
			"versionNonce": 1086188715,
			"isDeleted": false,
			"id": "tQoVVb54",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -448.9174496449664,
			"y": -622.1357272656521,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 489.990966796875,
			"height": 144.12866595267812,
			"seed": 1973417611,
			"groupIds": [
				"MnhJvKDDKLrWiaqf1ymgV"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"fontSize": 25.06585494829185,
			"fontFamily": 2,
			"text": "function () {\n    console.log(this.name)\n} \n例如上面等于的匿名函数为fn\n注意不是fn()，有小括号就是执行了这个函数",
			"rawText": "function () {\n    console.log(this.name)\n} \n例如上面等于的匿名函数为fn\n注意不是fn()，有小括号就是执行了这个函数",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "function () {\n    console.log(this.name)\n} \n例如上面等于的匿名函数为fn\n注意不是fn()，有小括号就是执行了这个函数",
			"lineHeight": 1.15,
			"baseline": 138
		},
		{
			"type": "rectangle",
			"version": 421,
			"versionNonce": 602195845,
			"isDeleted": false,
			"id": "2bbs8AgJScrIApVK9mzOT",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -469.43380876115987,
			"y": -632.2881161155372,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 525.1061177712318,
			"height": 166.2165027049317,
			"seed": 1345438469,
			"groupIds": [
				"MnhJvKDDKLrWiaqf1ymgV"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 918,
			"versionNonce": 1767373925,
			"isDeleted": false,
			"id": "rgRLipi8",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -720.4280235994529,
			"y": 104.23085462296552,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 406.487060546875,
			"height": 258.82203875047713,
			"seed": 797845029,
			"groupIds": [
				"MeEcrmIL8ldKdLnxncpgp"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730445751402,
			"link": null,
			"locked": false,
			"fontSize": 20.460240217429025,
			"fontFamily": 2,
			"text": "person1.foo3.call(person2) 表示打印的话\nfoo3: function () {\n    console.log (this)// person2\n    return fn\n}\n调用了foo3方法，return得到 fn\n函数内部存在this，call 显式绑定了person2\n\nperson.foo3.call(person2)()\n这个表示的就是fn(),执行了foo3属性的方法，\n返回了fn，后面()在执行返回的函数就是fn()",
			"rawText": "person1.foo3.call(person2) 表示打印的话\nfoo3: function () {\n    console.log (this)// person2\n    return fn\n}\n调用了foo3方法，return得到 fn\n函数内部存在this，call 显式绑定了person2\n\nperson.foo3.call(person2)()\n这个表示的就是fn(),执行了foo3属性的方法，\n返回了fn，后面()在执行返回的函数就是fn()",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "person1.foo3.call(person2) 表示打印的话\nfoo3: function () {\n    console.log (this)// person2\n    return fn\n}\n调用了foo3方法，return得到 fn\n函数内部存在this，call 显式绑定了person2\n\nperson.foo3.call(person2)()\n这个表示的就是fn(),执行了foo3属性的方法，\n返回了fn，后面()在执行返回的函数就是fn()",
			"lineHeight": 1.15,
			"baseline": 253
		},
		{
			"type": "rectangle",
			"version": 414,
			"versionNonce": 1651807845,
			"isDeleted": false,
			"id": "7-DXTKXBcdRVP4_C59CAb",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -731.6669364054083,
			"y": 98.17910037838953,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 418.44305551245196,
			"height": 274.7821004034817,
			"seed": 1754310219,
			"groupIds": [
				"MeEcrmIL8ldKdLnxncpgp"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 515,
			"versionNonce": 1165230373,
			"isDeleted": false,
			"id": "ydX6ttVn_3uD9smadX5ru",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -136.90987739676962,
			"y": 237.75717138120223,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 175.31400349618661,
			"height": 2.2611353095396964,
			"seed": 504521003,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730445755965,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-175.31400349618661,
					2.2611353095396964
				]
			]
		},
		{
			"type": "text",
			"version": 45,
			"versionNonce": 1615071371,
			"isDeleted": false,
			"id": "Vtmxo5pn",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 185.91180690741714,
			"y": 227.35213465216407,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 79.99993896484375,
			"height": 23,
			"seed": 1203824075,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "默认绑定",
			"rawText": "默认绑定",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "默认绑定",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 153,
			"versionNonce": 1011276197,
			"isDeleted": false,
			"id": "zmBpqFTBqd0Hs8BkVCYD9",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -138.60001695320034,
			"y": 252.42552844826736,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 300.00437475940953,
			"height": 18.591767229626612,
			"seed": 662465163,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 598,
			"versionNonce": 724894181,
			"isDeleted": false,
			"id": "29virnGI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -415.1503424401172,
			"y": 412.29470031167716,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 420.59954833984375,
			"height": 138,
			"seed": 1876729317,
			"groupIds": [
				"Y0XyonXR2jphXgb32xrKJ"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730447102094,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "person1.foo3() 等价与 fn\n执行了foo3的方法，return 了fn\n\nperson1.foo3().call(person2) = fn.call(person2)\n这是一个显示绑定，对返回的fn的一个绑定调用\n所以显式绑定 - person2 ",
			"rawText": "person1.foo3() 等价与 fn\n执行了foo3的方法，return 了fn\n\nperson1.foo3().call(person2) = fn.call(person2)\n这是一个显示绑定，对返回的fn的一个绑定调用\n所以显式绑定 - person2 ",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "person1.foo3() 等价与 fn\n执行了foo3的方法，return 了fn\n\nperson1.foo3().call(person2) = fn.call(person2)\n这是一个显示绑定，对返回的fn的一个绑定调用\n所以显式绑定 - person2 ",
			"lineHeight": 1.15,
			"baseline": 133
		},
		{
			"type": "rectangle",
			"version": 362,
			"versionNonce": 459636037,
			"isDeleted": false,
			"id": "D2m8Vd-ijkTYrHXmb9hcZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -425.46176577892305,
			"y": 413.1422690424912,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 454.03221565230183,
			"height": 145.88315569596773,
			"seed": 245504587,
			"groupIds": [
				"Y0XyonXR2jphXgb32xrKJ"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 506,
			"versionNonce": 2025893893,
			"isDeleted": false,
			"id": "A3B5Gubnd-JxP8WxZrwgT",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -117.07229831619259,
			"y": 274.52970030573385,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 208.5498889503732,
			"height": 133.9318242454965,
			"seed": 1449738405,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730447102094,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-208.5498889503732,
					133.9318242454965
				]
			]
		},
		{
			"type": "rectangle",
			"version": 94,
			"versionNonce": 662598757,
			"isDeleted": false,
			"id": "0XWBjr2t0tOKh8ztlyjD3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -131.2788983672059,
			"y": 300.1435461767681,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 135.74159024656456,
			"height": 17.162682186294546,
			"seed": 630472331,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 155,
			"versionNonce": 1049750283,
			"isDeleted": false,
			"id": "oLnRem64",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 107.78854370564315,
			"y": -622.8997479887881,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 454.22186279296875,
			"height": 137.38255982033547,
			"seed": 2143245515,
			"groupIds": [
				"lXlmcFLLxw1-G4HBDDxgv"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false,
			"fontSize": 23.892619099188778,
			"fontFamily": 2,
			"text": "() => {\n    console.log(this.name)\n}\n例如上面的箭头函数为wn\n注意不是wn()，有小括号就是执行了这个函",
			"rawText": "() => {\n    console.log(this.name)\n}\n例如上面的箭头函数为wn\n注意不是wn()，有小括号就是执行了这个函",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "() => {\n    console.log(this.name)\n}\n例如上面的箭头函数为wn\n注意不是wn()，有小括号就是执行了这个函",
			"lineHeight": 1.15,
			"baseline": 132
		},
		{
			"type": "rectangle",
			"version": 136,
			"versionNonce": 471752485,
			"isDeleted": false,
			"id": "nCmYZAzV8pvSKDdiuMUHq",
			"fillStyle": "solid",
			"strokeWidth": 4,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 81.78991254462949,
			"y": -637.5945960994247,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 525.6231047123038,
			"height": 168.42548520968893,
			"seed": 1069897221,
			"groupIds": [
				"lXlmcFLLxw1-G4HBDDxgv"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445375872,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 732,
			"versionNonce": 1863724293,
			"isDeleted": false,
			"id": "85W6Jx7BNiqvzx_NvSAHG",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -23.239531684836265,
			"y": 305.7772736448439,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 498.326478567334,
			"height": 340.62122810085714,
			"seed": 2024307461,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730447004788,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": {
				"elementId": "SHUuSF6M",
				"focus": 0.852550882089212,
				"gap": 3.9387586996857635
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					498.326478567334,
					-340.62122810085714
				]
			]
		},
		{
			"type": "text",
			"version": 738,
			"versionNonce": 623946149,
			"isDeleted": false,
			"id": "SHUuSF6M",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 479.0257055821835,
			"y": -50.87885615986312,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 233.1798095703125,
			"height": 23,
			"seed": 804867787,
			"groupIds": [
				"-nmUJWVw0BSQGVBGsI6XN"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "85W6Jx7BNiqvzx_NvSAHG",
					"type": "arrow"
				}
			],
			"updated": 1730447004788,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价于放回的箭头函数 wn",
			"rawText": "等价于放回的箭头函数 wn",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价于放回的箭头函数 wn",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 690,
			"versionNonce": 473187429,
			"isDeleted": false,
			"id": "nbrBLIGSMw8g8ZlxFrFEd",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 473.19446827271497,
			"y": -70.79139349396456,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 259.2617730065447,
			"height": 58.665017712070494,
			"seed": 250701733,
			"groupIds": [
				"-nmUJWVw0BSQGVBGsI6XN"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730447004788,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 174,
			"versionNonce": 1089869995,
			"isDeleted": false,
			"id": "KyyDK-ytD_PwK6a-KUbFx",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -133.64288159089298,
			"y": 295.6698036352478,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 178.09882120667496,
			"height": 23.567970320086204,
			"seed": 1970488971,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445406250,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 309,
			"versionNonce": 960715813,
			"isDeleted": false,
			"id": "hdsyD5jr",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 485.21314767345825,
			"y": 18.42417450972357,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 106.01991271972656,
			"height": 23,
			"seed": 799263563,
			"groupIds": [
				"y-UPCbc786RDXEr8MFfZG"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730447002607,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价于 wn()",
			"rawText": "等价于 wn()",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价于 wn()",
			"lineHeight": 1.15,
			"baseline": 18
		},
		{
			"type": "rectangle",
			"version": 331,
			"versionNonce": 53383045,
			"isDeleted": false,
			"id": "9sc4RWpOrl8SRYA_0j2TT",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 479.33853239101154,
			"y": 8.353317643197556,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 129.24261189739013,
			"height": 40.28342746610406,
			"seed": 195284645,
			"groupIds": [
				"y-UPCbc786RDXEr8MFfZG"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 397,
			"versionNonce": 68966117,
			"isDeleted": false,
			"id": "OgOuhmCeMYHCxIFOcwSGF",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 42.579287766751236,
			"y": 299.9925580802651,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 435.1609420957412,
			"height": 250.84309165231076,
			"seed": 1158293157,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730447002607,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": {
				"elementId": "9sc4RWpOrl8SRYA_0j2TT",
				"focus": 0.30521805423673165,
				"gap": 1.6785273674479413
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					435.1609420957412,
					-250.84309165231076
				]
			]
		},
		{
			"type": "rectangle",
			"version": 187,
			"versionNonce": 1403613451,
			"isDeleted": false,
			"id": "yMgWJKxr2jLDr9aQeiqmQ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -132.65182196572482,
			"y": 319.89833179615295,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 311.90719720378195,
			"height": 25.13106856044709,
			"seed": 788493515,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730445489424,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 503,
			"versionNonce": 511814085,
			"isDeleted": false,
			"id": "xgbC6oiJ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 519.047100296532,
			"y": 72.59714758068435,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 461.2197265625,
			"height": 276,
			"seed": 1460475819,
			"groupIds": [
				"z38JZOthW4vPK0bm_v01p"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1730446991903,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "person1.foo4.call(person2) 表示打印的话\nfoo4: funtion () {\n    console.log(this) //person2\n    reurn wn\n}\n调用了foo4方法，return得到wn\n函数内部存在this，call 显式绑定了person2\n\nperson1.foo4.call(person2)() 等价与 wn()\n\nwn是一个箭头函数里面this作用域，向外找到外层的\n函数内部显式绑定的 person2",
			"rawText": "person1.foo4.call(person2) 表示打印的话\nfoo4: funtion () {\n    console.log(this) //person2\n    reurn wn\n}\n调用了foo4方法，return得到wn\n函数内部存在this，call 显式绑定了person2\n\nperson1.foo4.call(person2)() 等价与 wn()\n\nwn是一个箭头函数里面this作用域，向外找到外层的\n函数内部显式绑定的 person2",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "person1.foo4.call(person2) 表示打印的话\nfoo4: funtion () {\n    console.log(this) //person2\n    reurn wn\n}\n调用了foo4方法，return得到wn\n函数内部存在this，call 显式绑定了person2\n\nperson1.foo4.call(person2)() 等价与 wn()\n\nwn是一个箭头函数里面this作用域，向外找到外层的\n函数内部显式绑定的 person2",
			"lineHeight": 1.15,
			"baseline": 271
		},
		{
			"type": "rectangle",
			"version": 151,
			"versionNonce": 1922181413,
			"isDeleted": false,
			"id": "t2KZFdx-dL5qk5Y0_nJDI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 497.16376067628084,
			"y": 61.995509051558486,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 503.30381590772686,
			"height": 289.52318721222827,
			"seed": 64968235,
			"groupIds": [
				"z38JZOthW4vPK0bm_v01p"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "arrow",
			"version": 146,
			"versionNonce": 589020293,
			"isDeleted": false,
			"id": "tm1Q5CGILFJciijvyY_XD",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 177.80988495304985,
			"y": 323.7368168258515,
			"strokeColor": "#2f9e44",
			"backgroundColor": "transparent",
			"width": 318.353875723231,
			"height": 94.67229944805587,
			"seed": 615928747,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730446991903,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": {
				"elementId": "t2KZFdx-dL5qk5Y0_nJDI",
				"gap": 1,
				"focus": 0.24055949392036993
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					318.353875723231,
					-94.67229944805587
				]
			]
		},
		{
			"type": "rectangle",
			"version": 116,
			"versionNonce": 1432483883,
			"isDeleted": false,
			"id": "NDoBOJLpWEeHYXrnjeUut",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -135.8031215829471,
			"y": 346.35467217424514,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 314.9665523146823,
			"height": 26.591076632122167,
			"seed": 1180429253,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 826,
			"versionNonce": 277330283,
			"isDeleted": false,
			"id": "rnHmBdq3",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 226.16159324504815,
			"y": 382.6720212772146,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 522.4395751953125,
			"height": 207,
			"seed": 1103953893,
			"groupIds": [
				"ux-FA54TzR2_fZHBQg5UO"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "vic2k3yylI6UsoVoEw_KZ",
					"type": "arrow"
				}
			],
			"updated": 1730446976224,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "person1.foo4()等价于 wn\n() 说明调用了foo4的方法 ，通过return返回了 wn\n\nperson1.foo4().call(person2) 等价wn.call(person2)\n显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数\n没有this的作用域，所以显式调用没有用\n\nwn（）显式绑定无效，外层的函数存在this，并且这个this\n隐式绑定了 person1，所以上层作用域 - person1",
			"rawText": "person1.foo4()等价于 wn\n() 说明调用了foo4的方法 ，通过return返回了 wn\n\nperson1.foo4().call(person2) 等价wn.call(person2)\n显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数\n没有this的作用域，所以显式调用没有用\n\nwn（）显式绑定无效，外层的函数存在this，并且这个this\n隐式绑定了 person1，所以上层作用域 - person1",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "person1.foo4()等价于 wn\n() 说明调用了foo4的方法 ，通过return返回了 wn\n\nperson1.foo4().call(person2) 等价wn.call(person2)\n显式绑定了 wn 的 this 指向 person2，但是 wn 是箭头函数\n没有this的作用域，所以显式调用没有用\n\nwn（）显式绑定无效，外层的函数存在this，并且这个this\n隐式绑定了 person1，所以上层作用域 - person1",
			"lineHeight": 1.15,
			"baseline": 202
		},
		{
			"type": "rectangle",
			"version": 326,
			"versionNonce": 1908411723,
			"isDeleted": false,
			"id": "PB11YUXrZrjsJL8HkjiVg",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 212.06650153228452,
			"y": 382.6720212772143,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 546.401943979285,
			"height": 211.43017118367857,
			"seed": 208515301,
			"groupIds": [
				"ux-FA54TzR2_fZHBQg5UO"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730446976225,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 346,
			"versionNonce": 301111979,
			"isDeleted": false,
			"id": "vic2k3yylI6UsoVoEw_KZ",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 180.71739422924117,
			"y": 374.5922707249743,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 41.298610597880554,
			"height": 21.070619031876845,
			"seed": 154104581,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730446976225,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					41.298610597880554,
					21.070619031876845
				]
			]
		},
		{
			"type": "rectangle",
			"version": 179,
			"versionNonce": 1887322859,
			"isDeleted": false,
			"id": "Wj4Y7OOnzsxxPK4gIm6jI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -138.16473813297983,
			"y": -154.8433619761983,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 367.30807600797186,
			"height": 139.29520955828679,
			"seed": 1931051435,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
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
			"type": "text",
			"version": 134,
			"versionNonce": 86106117,
			"isDeleted": false,
			"id": "SZQUba72",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 502.7589294343028,
			"y": -202.93334904476694,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 160.55984497070312,
			"height": 92,
			"seed": 1836723083,
			"groupIds": [
				"e4gFd0-HoCZ9xQU-Iom0B"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "2unM3VXMMNOMp0Q7jqIPE",
					"type": "arrow"
				}
			],
			"updated": 1730447072259,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 2,
			"text": "等价于\nfoo4: function () {\n    return wn\n}",
			"rawText": "等价于\nfoo4: function () {\n    return wn\n}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "等价于\nfoo4: function () {\n    return wn\n}",
			"lineHeight": 1.15,
			"baseline": 87
		},
		{
			"type": "rectangle",
			"version": 146,
			"versionNonce": 985973285,
			"isDeleted": false,
			"id": "FpXk_W5CrSd9jrgpuFgzt",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 481.20129274626674,
			"y": -216.1995432124943,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 204.7971689871202,
			"height": 114.4210717719717,
			"seed": 815561157,
			"groupIds": [
				"e4gFd0-HoCZ9xQU-Iom0B"
			],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1730447072260,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 190,
			"versionNonce": 391340741,
			"isDeleted": false,
			"id": "2unM3VXMMNOMp0Q7jqIPE",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 230.80158842413158,
			"y": -65.83631559502582,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 256.20369510889014,
			"height": 84.55772032129268,
			"seed": 309087717,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1730447072260,
			"link": null,
			"locked": false,
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
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					256.20369510889014,
					-84.55772032129268
				]
			]
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
		"scrollX": 848.0996799107003,
		"scrollY": 1286.746201819266,
		"zoom": {
			"value": 0.4
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