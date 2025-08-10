# 一、认识 ES Module
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743939510000dqvnjg.png)

# 二、案例代码结构组件
在浏览器中演示ES6的模块化开发：

```html
<script src="./bar.js" type="module"></script>
<script src="./main.js" type="module"></script>
```

如果直接在浏览器中运行代码，会报如下错误：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743940725000apu56j.png)

这个在MDN上面有给出解释： 

* https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Modules 
* 需要注意本地测试 — 如果你通过本地加载Html 文件 (比如一个 file:// 路径的文件), 你将会遇到 CORS 错误，因为 Javascript 模块安全性需要； 
	* CORS是一种协议，
* 你需要通过一个服务器来测试； 

> 在浏览器中使用 ES module 的时候，进行 import 导入的时候会去下载解析导入的文件，这里里面就会使用到 CORS 协议。

**我这里使用的VSCode插件：Live Server**

导出设置：

```js
const name = "axl"
const age = 18
  
function sayHello() {
 console.log("sayHello")
}
  
// export 关键字进行导出
export { name, age, sayHello}
```


导入设置：

```js
// import 关键字进行导入
// 使用解构来进行解构
import { name, age, sayHello} from "./bar.js"

console.log(name, age, sayHello)
```


# 三、export关键字
export关键字将一个模块中的变量、函数、类等导出； 

我们希望将其他中内容全部导出，它可以有如下的方式： 

* **方式一**：在语句声明的前面直接加上export关键字 

```js
export const name = "axl"
export const age = 18
  
export function sayHello() {
 console.log("sayHello")
}
```

* **方式二**：将所有需要**导出的标识符**，放到export后面的 {}中 
	* **注意**：这里的 {}里面**不是ES6的对象字面量的增强写法**，{}也**不是**表示一个**对象**的； 
	* 所以：` export {name: name}`，是错误的写法； 
	* 实际里面导出的是表示的是标识符 `export {标识符1,标识符2,……}`

```js
const name = "axl"
const age = 18
  
function sayHello() {
 console.log("sayHello")
}
  
// 正确导出
export { name, age, sayHello}
  
// 错误导出
// export { name: "axl"}
```

* **方式三**：导出时给标识符起一个别名 
	* 通过as关键字起别名


```js
export {
 name as bname,
 age as bage,
 sayHello as bsayHello
}
```


# 四、import 关键字
import关键字负责从另外一个模块中导入内容 :**没有在webpack中时，导入的文件夹必须加上文件后缀，如：.js**

导入内容的方式也有多种： 

* 方式一：import {标识符列表} from '模块'；
	* 注意：这里的{}也不是一个对象，里面只是**存放导入的标识符列表内容**；
* 方式二：导入时给标识符起别名 
	* 通过as关键字起别名 
* 方式三：通过 `*` 将模块功能放到一个模块功能对象`（a module object）`上

```js
// 方式一：
import { name, age, sayHello} from "./bar.js"
  
// 方式二：
import { name as bname, age as bage, sayHello as bsayHello} from "./bar.js"
  
// 方式三：
import * as foo from "./bar.js"
```


# 五、export和import结合使用
补充:export和import可以结合使用

```js
export { sum as barSum } from './bar.js';
```

**为什么要这样做呢?**

* 在开发和封装一个功能库时，通常我们希望将暴露的<mark class="hltr-orange">所有接口放到一个文件中</mark>;
* 这样方便指定统一的接口规范，也方便阅读，
* 这个时候，我们就可以使用export和import结合使用;

例如当存在 utils 文件夹， 里面有很多工具的时候，就会把这些所有的工具全部放到 index.js 文件里面放进行一个统一的导出。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743943731000f2hfjp.png)

这样就可以使用一个文件来进行所有的文件进行导入和导出。

```js
// 其中一种的导入方式，也可以是使用其他的导入方式
import * as foo from './utils/index.js'
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1743943950000t5bl9c.png)

但是在 index.js 导出的时候还是有点麻烦，可以**进行一个优化**：

```js
export * from './01工具1.js'
export * from './01工具2.js'
```

> 从 form 导入，并且从 export 导出全部数据，也可以理解为是一种简化的编写。
> 当然也是可以特定导出的。

```js
export { name, age } from './01工具1.js'
```

# 六、default用法
前面的导出功能都是有**名字的导出（named exports）**： 

* 在导出export时指定了名字； 
* 在导入import时需要知道具体的名字；

还有一种导出叫做**默认导出（default export）** 

* 默认导出export时可以**不需要指定名字**； 
* 在**导入时不可以使用 {}**，并且可**以自己来指定名字；**
* 它也方便我们和现有的CommonJS等规范相互操作；

> [!important] 注意：
在一个模块中，**只能有一个默认导出（default export）**；

## 6.1 第一种导入和导出
导出和导入相同的名字

```js
function sayHello () {
 console.log("sayHello")
} 

export default sayHello
```

```js
import sayHello from "./utles.js";
sayHello()//sayHello
```

## 6.2 第二种导入和导出
**导出匿名的标识符，导入任意命名标识符。**

```js
// 导出匿名标识符
export default function() {
 console.log("sayHello")
}
```

```js
// 匿名导出的，所有在导入的时候可以随便起名标识符
import a from './utles.js'
a()//sayHello
```

# 七、import 函数
通过import关键字加载一个模块，是不可以在其放到逻辑代码中的，比如： 

```js
if (true) {
 import sayHello from "./utles.js"
}
//Uncaught SyntaxError: Unexpected identifier 'sayHello' (at main.js:8:9)
// unexpected 意外的
// identifier 标识符
```

**为什么会出现这个情况呢？** 

* 这是因为ES Module在被JS引擎解析时，就**必须知道它的依赖关系**； 
* 由于这个时候js代码没有任何的运行，所以无法在进行**类似于if判断中根据代码的执行情况**； 
* 甚至**拼接路径的写法也是错误**的：因为我们必须到运行时能确定path的值； 

但是某些情况下，我们确确实实希望动态的来加载某一个模块： 

* 如果根据不同的条件，动态来选择加载模块的路径； 
* 这个时候我们需要使用 import() 函数来动态加载； 
	* **import函数返回一个Promise，可以通过then获取结果**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1744026562000clzi7c.png)

# 八、emport meta(了解)
import.meta是一个给JavaScript模块暴露特定上下文的元数据属性的对象。

* 它包含了这个模块的信息，比如说这个模块的URL； 
* 在ES11（ES2020）中新增的特性；


```js
import sayHello from "./utles.js";

console.log(import.meta)
//{url: 'http://127.0.0.1:5500/02%20%E5%89%8D%E7%AB%AF%E6%A…C%96%E5%BC%80%E5%8F%91/05%20ES%20module02/main.js', resolve: ƒ}
```



