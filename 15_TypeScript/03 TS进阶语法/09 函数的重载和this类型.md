# 一、函数的重载(了解)

## 1.1 认识函数重载

在TypeScript中，如果我们编写了一个add函数，希望可以对字符串和数字类型进行相加，应该如何编写呢？ 

可能会这样来编写，但是其实是错误的：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760273927000jufaom.png)

那么这个代码应该如何去编写呢？ 

- 在TypeScript中，我们可以去编写不同的**重载签名（overload signatures）** 来表示函数可以**以不同的方式进行调用**； 
- 一般是**编写两个或者以上的重载签名**，再去**编写一个通用的函数以及实现**；

## 1.2 sum函数的重载

如我们对sum函数进行重构： 在调用sum的时候，它会**根据传入的参数类型来决定执行函数体**，来决定到底执行哪一个函数的重载签名；

```ts
//编写重载签名
function sum(num1:number, num2:number):number
function sum(num1:string, num2:string):string

//编写通用函数
function sum(sum1:any, sum2: any) {
  return sum1 + sum2
}

console.log(sum(10, 20))//30
console.log(sum("coder", "axl"))//coderaxl
console.log(sum('axl', 123))//错误的
```

但是注意，有实现体的函数，是不能直接调用的：

```ts
//下面是错误的调用
//sum()
//sum({name: "axl"}, {age: 123})
```

## 1.3 联合类型vs重载

我们现在有一个需求：定义一个函数，可以**传入字符串或者数组**，获取它们的长度。 

这里有两种实现方案： 

- 方案一：使用联合类型来实现； 
- 方案二：实现函数重载来实现；
- 方案三：使用[[02 JS数据类型#六、Object类型|对象类型]]来实现

```ts
//方案一
function getLength(a: any[] | string) {
  return a.length
}
```

```ts
//方案二
function getLength(a: string): number;
function getLength(a: any[]): number;

function getLength(a) {
  return a.length;
}
```

```ts
function getLength(a: { length: number }) {
  return a.length
}

getLength('123')
getLength([1, 2, 3])
getLength({ length: 10 })
```

> [!tip] 在开发中我们选择使用哪一种呢？ 
> 在可能的情况下，尽量选择使用联合类型来实现；


# 二、this类型

## 2.1 可推导的this类型

**当然在目前的Vue3和React开发中你不一定会使用到this**：  Vue3的Composition API中很少见到this，React的Hooks开发中也很少见到this了；

但是还是简单掌握一些TypeScript中的this，TypeScript是如何处理this呢？我们先来看两个例子：

```ts
//第一个
const obj = {
  name: 'axl',
  getName: function () {
    console.log(this.name)
  }
}
obj.getName()//axl
```

上面的代码默认情况下是可以正常运行的，也就是TypeScript在编译时，认为我们的this是可以正确去使用的： 这是因为**在没有指定this的情况，this会更具上下文[[01 TS变量声明#三、变量的类型推导(推断)|推导]]出来this的类型**；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760277517000kvj01d.png)

## 2.2 this的编译选择

VSCode在检测我们的TypeScript代码时，默认情况下运行不确定的this也是会报错的，例如下面的代码：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760341771000dgjmgt.png)

> [!tip]
> 在以前的 TS 版本中，上面的这个代码并不会进行报错，会推导出来 this 的类型为 any 类型，并不会报错。
> 
> 如果要报错的话，必须是严格模式，在 `tsconfig.json` 中设置 `"strict": true` 或 `"noImplicitThis": true`

到了现在，即使没有 `tsconfig.json` ，较新版本的 TypeScript 默认会启用一些严格检查。从 TypeScript 2.3 开始，某些检查在**默认情况下就是启用**的。

我们可以创建一个tsconfig.json文件，并且在其中显示的告知VSCodethis必须明确执行严格模式（**不能是隐式的**）；

初始化一个 tsconfig.json 文件：

```bash
tsc --init
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17603422140000e1668.png)

在设置了noImplicitThis为true时， TypeScript会根据上下文推导this，但是在不能正确推导时，就会报错，需要我们明确 的指定this。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760342647000h4vk5e.png)

## 2.3 指定this的类型

如何指定呢？函数的第一个参数类型： 

- 函数的**第一个参数**我们可以根据该函数之后被调用的情况，**用于声明this的类型（名词必须叫this）**； 
- 在后续调用函数传入参数时，从第二个参数开始传递的，this参数会在编译后被抹除；

```ts
function foo(this: any, name: string) {
  console.log(this, name)
}
foo('axl')
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760966276000j1fq0u.png)





