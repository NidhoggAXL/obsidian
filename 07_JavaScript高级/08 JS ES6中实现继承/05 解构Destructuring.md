# 一、认识解构
ES6中新增了一个从**数组或对象中方便获取数据**的方法，称之为解构Destructuring。 

* 解构赋值 是一种特殊的语法，它使我们可以将数组或对象“拆包”至一系列变量中。 

**我们可以划分为**：数组的解构和对象的解构。

## 1.1 数组解构

数组解构允许我们**按照索引位置提取值**。

**基本用法**：

```js
// 有一个存放了姓名和姓氏的数组
let arr = ["John", "Doe"];

// 解构赋值
// 将 arr[0] 赋值给 firstName，将 arr[1] 赋值给 lastName
let [firstName, lastName] = arr;

console.log(firstName); // John
console.log(lastName);  // Doe
```

**跳过元素**：可以使用逗号来忽略不需要的元素。

```js
let [a, , c] = ["foo", "bar", "baz"];

console.log(a); // foo
console.log(c); // baz (第二个元素 "bar" 被跳过了)
```

**使用 `...` 剩余操作符:** 可以使用剩余模式 `...` 将数组的剩余部分收集到另一个数组中。

```js
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

console.log(name1); // Julius
console.log(name2); // Caesar
console.log(rest); // ["Consul", "of the Roman Republic"]
console.log(rest[0]); // Consul
console.log(rest.length); // 2
```

**默认值：** 如果数组的值少于变量的数量，或者某个位置的值为 `undefined`，你可以为变量提供默认值。

```js
let [firstName = "Guest", lastName = "Anonymous"] = ["John"];

console.log(firstName); // John (来自数组)
console.log(lastName);  // Anonymous (使用了默认值)

let [a = 1, b = 2] = [undefined, 5];
console.log(a); // 1 (因为第一个值是 undefined，所以使用默认值)
console.log(b); // 5 (来自数组)
```

**交换变量值：** 解构赋值是交换两个变量值的经典技巧，无需临时变量。

```js
let a = 1;
let b = 3;

[a, b] = [b, a]; // 交换

console.log(a); // 3
console.log(b); // 1
```

## 1.2 对象解构

对象解构允许我们<mark class="hltr-cyan">按照属性名提取值</mark>。

**基本用法：**

```js
// 有一个用户对象
let user = {
  name: "John",
  age: 30
};

// 解构赋值
// 将 user.name 赋值给变量 name，将 user.age 赋值给变量 age
let {name, age} = user;

console.log(name); // John
console.log(age);  // 30
```

> [!note] 这里的变量 `name` 和 `age` 必须与对象中的属性名一致。

**重命名变量:** 如果你不想使用对象中的属性名作为变量名，可以使用冒号 `:` 来重命名。

```JS
let user = {
  name: "John",
  age: 30
};

// { 原属性名: 新的变量名 }
let {name: userName, age: userAge} = user;

console.log(userName); // John
console.log(userAge);  // 30
// 此时 name 和 age 不再是变量，会报错
// console.log(name); // ReferenceError
```

**默认值**：和数组一样，你也可以为对象的属性提供默认值，以防该属性不存在或其值为 `undefined`。

```JS
let user = {
  name: "John"
};

let {name, age = 18, isAdmin = false} = user;

console.log(name);     // John
console.log(age);      // 18 (因为原对象中没有 age，使用默认值)
console.log(isAdmin);  // false (因为原对象中没有 isAdmin，使用默认值)
```

**使用 `...` 剩余操作符:** 可以使用剩余模式 `...` 将对象的剩余部分收集到另一个对象中。

```JS
const info = {
  name: 'axl',
  age: 18,
  firends: {
    name: 'kobe',
    age: 30
  },
  lever: 99
}

let { name, age, ...rest } = info

console.log(name)//axl
console.log(age)//18

console.log(rest)
//{ firends: { name: 'kobe', age: 30 }, lever: 99 }
```

**结合重命名和默认值**：你可以同时使用重命名和默认值。

```JS
let options = {
  title: "Menu"
};

let {title: header = "Untitled", width: w = 100, height: h = 200} = options;

console.log(header); // Menu (来自 options.title)
console.log(w);      // 100 (options 中没有 width，使用默认值)
console.log(h);      // 200 (options 中没有 height，使用默认值)
```

**嵌套对象解构**:对于嵌套的对象，解构也可以同样处理。

```JS
let company = {
  name: "Tech Corp",
  location: {
    city: "San Francisco",
    state: "CA"
  }
};

// 注意外层的 {} 和解构内层的 {} 的模式
let {
  name,
  location: { city, state } // 将 company.location.city 提取到变量 city
} = company;

console.log(name); // Tech Corp
console.log(city); // San Francisco
console.log(state); // CA
// location 本身没有被赋值，它只是一个用于定位的模式
// console.log(location); // ReferenceError

```

如果你想同时提取 `location` 本身，可以这样做：

```JS
let {
  name,
  location,        // 将 company.location 赋值给变量 location
  location: { city, state } // 同时解构 location 内部的属性
} = company;

console.log(location); // { city: 'San Francisco', state: 'CA' }
console.log(city);     // San Francisco
```


# 二、解构的应用场景

**解构目前在开发中使用是非常多的**： 

* 比如在开发中拿到一个变量时，自动对其进行解构使用； 

```JS
const { name, age } = infos
```

* 比如对函数的参数进行解构；

```JS
// 一个接收配置对象的函数，没有解构
function showMenu(options) {
  let title = options.title || "Untitled";
  let width = options.width || 100;
  let height = options.height || 200;
  // ... 其他逻辑
}

// 使用参数解构，清晰且简洁
function showMenu({ title = "Untitled", width = 100, height = 200, items = [] }) {
  console.log(`${title} ${width} ${height}`); // My Menu 150 200
  console.log(items); // ["Item1", "Item2"]
}

// 调用函数并传入一个对象
// 只传递部分参数，其余使用默认值
showMenu({
  title: "My Menu",
  width: 150,
  items: ["Item1", "Item2"]
});
```

**为了确保即使不传参数也不会报错（即 `undefined` 被解构），你可以为整个参数设置一个空对象 `{}` 作为默认值。**

```JS
function showMenu({ title = "Untitled", width = 100 } = {}) {
  console.log(title, width);
}

showMenu(); // Untitled 100 (安全调用，不会报错)
// 如果没有 `= {}`，直接调用 showMenu() 会抛出错误
```
