# 一、认识TS的内置工具

Typescript 提供了一些工具类型来辅助进行**常见的类型转换**，这些类型全局可用。

# 二、关于this的内置工具

## 2.1 ThisParameterType

**ThisParameterType**： 

- 用于提取一个函数类型Type的this (opens new window)参数类型； 
- 如果这个函数类型没有this参数返回unknown；

```ts
function foo(this: {name: string}, age: number) {
  console.log(this.name)
}

//用于获取一个函数的this类型
type ThisType = ThisParameterType<typeof foo>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760345777000bvo1s4.png)

## 2.2 OmitThisParameter

**OmitThisParameter**：  用于移除一个函数类型Type的this参数类型, 并且返回当前的函数类型

```ts
function foo(this: {name: string}, age: number) {
  console.log(this.name)
}

//用于移除函数的this参数类型，并且返回当前函数类型
type Foo = OmitThisParameter<typeof foo>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1760345871000sxhzrf.png)

## 2.3 ThisType

**ThisType：**  这个类型不返回一个转换过的类型，它被用作**标记一个上下文的this类型**。（官方文档） 

TypeScript 中的 `ThisType` 是一个非常有用的工具类型，主要用于在**对象字面量**中控制其方法的 `this` 上下文类型。当你需要为一个对象字面量中的方法指定特定的 `this` 类型，而这些方法本身没有显式声明 `this` 类型时，`ThisType` 就派上用场了。

下面这个表格汇总了 `ThisType` 的核心用途：

|特性|说明|
|---|---|
|**主要作用**|标记对象字面量方法中 `this` 的类型|
|**使用方式**|通过类型交叉（`&`）为对象字面量增加 `this` 类型标记|
|**典型场景**|框架开发（如 Vue 2）、库函数封装、复杂对象配置|
|**类型安全**|配合 `noImplicitThis` 编译选项，可更严格检查 `this` 类型|

### 🎯 主要作用

`ThisType<T>` 的核心作用是**为一个对象字面量中所有函数方法的 `this` 上下文提供统一的类型标记**。它本身是一个空接口，TypeScript 编译器会识别这个类型标记，并将该类型注入到对象所有方法的 `this` 上下文中。

这意味着，当你使用 `ThisType<T>` 后，对象方法内的 `this` 就会被 TypeScript 识别为 `T` 类型，从而获得完整的类型检查和代码自动补全。


### 🔦 使用示例

#### 基础用法

```ts
interface MyContext {
  logError: (error: string) => void;
  count: number;
}

// 使用 ThisType 指定 helperFunctions 对象方法中的 this 类型
let helperFunctions: { [name: string]: Function } & ThisType<MyContext> = {
  hello: function() {
    this.logError("Error: Something went wrong!"); // √ TypeScript 知道 logError 是 MyContext 的一部分
    console.log(this.count); // √ 可以访问 count
    this.update(); // × 报错：Property 'update' does not exist on type 'MyContext'
  }
};
```

在这个例子中，虽然 `hello` 方法没有显式声明 `this` 类型，但由于 `helperFunctions` 变量被标记为 `& ThisType<MyContext>`，所以方法内的 `this` 自动被识别为 `MyContext` 类型。

#### 在框架中的应用（例如 Vue 2）

Vue 2 的选项式 API 就使用了 `ThisType` 来让组件的 `methods` 中的函数能访问 `data` 里的数据和其他方法：

```ts
// 类似 Vue 2 的类型设计
type Data = { message: string };
type Methods = { greet(): void };

const options: {
  data: Data,
  methods: Methods,
} & ThisType<Data & Methods> = { // 合并 Data 和 Methods 作为 this 类型
  data: {
    message: 'Hello'
  },
  methods: {
    greet() {
      console.log(this.message); // √ this 上有 message 和 greet
      this.greet(); // √ 可以调用其他方法
    }
  }
};
```

### ⚠️ 重要说明

使用 `ThisType<T>` 时，有几点需要特别注意：

1. **仅影响对象字面量**：`ThisType<T>` 只对直接包含它的对象字面量中的函数方法起作用。如果是类（class）的方法或者独立的函数，需要使用其他方式（如函数第一个参数声明 `this` 类型）来指定 `this` 类型。
    
2. **运行时无影响**：与所有 TypeScript 类型一样，`ThisType<T>` 只在编译时提供类型检查，**不会产生任何实际的 JavaScript 代码**。你需要确保在运行时，这些函数确实以正确的 `this` 上下文被调用（例如通过 `call`、`apply`、`bind` 或者作为对象的方法调用）。
    
3. **开启严格检查**：建议在 `tsconfig.json` 中开启 `"noImplicitThis": true`，这样 TypeScript 会对 `this` 的类型进行更严格的检查，帮助你发现潜在问题。
    

### 💎 总结

`ThisType<T>` 是 TypeScript 中的一个高级工具类型，它能优雅地解决对象字面量方法中 `this` 上下文的类型问题，尤其在编写或使用某些需要合并多个来源类型到 `this` 的框架或库时非常有用。

