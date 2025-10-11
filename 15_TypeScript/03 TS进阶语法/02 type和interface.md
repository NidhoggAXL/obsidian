# 一、类型别名

通过在类型注解中编写 **对象类型** 和 **联合类型**，但是当我们想要多次在其他地方使用时，就要编写多次。 

我们可以通过 type 给对象类型起一个别名：

```ts
type Point = { x: number , y: number }
function printPoint(point: Point) {
  console.log(point.x, point.y)
}
function sumPoint(point: Point) {
  console.log(point.x + point.y)
}
printPoint({ x: 1, y: 2 })// 1 2
sumPoint({ x: 1, y: 2 })// 3


type ID = number | string
function printID(id: ID) {
  console.log("你的id是", id)
}
printID("axl")//你的id是 axl
printID(123)//你的id是 123

```

# 二、接口声明

 前面通过type可以用来声明一个对象类型：

```ts
type Point = {
  name: string
  age: number
}
```

对象的另外一种声明方式就是通过接口来声明：

```ts
interface Point {
  name: string
  age: number
}
```

那么它们有什么区别呢？ 

- 类型别名和接口非常相似，在定义对象类型时，大部分时候，你可以任意选择使用。 
- 接口的几乎所有特性都可以在 type 中使用

# 三、type和interface的区别

## 3.1 基本语法

interface：

```ts
interface User {
  id: number;
  name: string;
  email: string;
}

interface Admin extends User {
  permissions: string[];
}
```

type：

```ts
type User = {
  id: number;
  name: string;
  email: string;
};

type Admin = User & {
  permissions: string[];
};
```

## 3.2 扩展方式

interface 使用 extends：

```ts
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

// 多重继承
interface ServiceDog extends Dog {
  training: string[];
}
```


type 使用交叉类型(&)：

```ts
type Animal = {
  name: string;
};

type Dog = Animal & {
  breed: string;
};

// 多重扩展
type ServiceDog = Dog & {
  training: string[];
};
```

## 3.3 声明合并(Declaration Merging)

interface 只是声明合并：

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

interface User {
  email: string;
}

// 最终合并为：
// interface User {
//   name: string;
//   age: number;
//   email: string;
// }

const user: User = {
  name: "John",
  age: 30,
  email: "john@example.com"
};
```


type 不支持声明合并：

```ts
type User = {
  name: string;
};

// ❌ 错误：重复标识符 "User"
type User = {
  age: number;
};
```

## 3.4 实现(implements)

两者都可以被类实现：

```ts
// 使用 interface
interface Printable {
  print(): void;
}

class Document implements Printable {
  print() {
    console.log("Printing document...");
  }
}

// 使用 type
type Serializable = {
  serialize(): string;
};

class Report implements Serializable {
  serialize() {
    return "Serialized data";
  }
}

// 同时实现多个
class AdvancedDocument implements Printable, Serializable {
  print() {
    console.log("Printing...");
  }
  
  serialize() {
    return "Data";
  }
}
```

## 3.5 高级类型功能

type 支持更复杂的类型：

```ts
// 联合类型
type ID = string | number;

// 元组类型
type Point = [number, number];

// 映射类型
type Optional<T> = {
  [K in keyof T]?: T[K];
};

// 条件类型
type IsString<T> = T extends string ? true : false;

// 模板字面量类型
type EventName = `on${string}`;
type HttpMethod = 'GET' | 'POST' | 'PUT' | 'DELETE';
```

interface 主要用于对象类型：

```ts
interface Point {
  x: number;
  y: number;
}

// interface 不能直接定义联合类型
// ❌ 错误
interface ID = string | number;
```

## 3.6 性能考虑

- **interface**：在大型代码库中，由于声明合并的特性，可能会有更好的性能
    
- **type**：对于复杂的条件类型和映射类型，可能会有更长的编译时间

## 3.7 实际使用场景

推荐使用 interface 的情况：

```ts
// 1. 对象形状定义
interface ApiResponse {
  data: any;
  status: number;
  message: string;
}

// 2. 类实现
interface DatabaseConnection {
  connect(): Promise<void>;
  disconnect(): Promise<void>;
}

// 3. 需要声明合并的库类型定义
interface Window {
  myCustomProperty: string;
}
```

推荐使用 type 的情况：

```ts
// 1. 联合类型
type Status = 'pending' | 'success' | 'error';

// 2. 元组类型
type Coordinates = [number, number, number?];

// 3. 复杂映射类型
type Readonly<T> = {
  readonly [K in keyof T]: T[K];
};

// 4. 函数类型
type ClickHandler = (event: MouseEvent) => void;

// 5. 从现有类型派生
type UserPartial = Partial<User>;
```

## 3.8 相互扩展

interface 扩张 type：

```ts
type Base = {
  id: number;
  createdAt: Date;
};

interface User extends Base {
  name: string;
  email: string;
}
```

type 扩张 interface：

```ts
interface Base {
  id: number;
  createdAt: Date;
}

type User = Base & {
  name: string;
  email: string;
};
```

## 3.9 总结

|特性|interface|type|
|---|---|---|
|声明合并|✅ 支持|❌ 不支持|
|扩展语法|`extends`|`&` (交叉类型)|
|类实现|✅ 支持|✅ 支持|
|联合类型|❌ 不支持|✅ 支持|
|元组类型|❌ 不支持|✅ 支持|
|映射类型|❌ 不支持|✅ 支持|
|性能|通常更好|复杂类型可能较慢|

**最佳实践**：

- 对于对象类型定义，优先使用 `interface`
    
- 对于联合类型、元组或复杂类型操作，使用 `type`
    
- 在项目中保持一致性，遵循团队约定