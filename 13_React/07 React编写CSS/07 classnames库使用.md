# 一、Vue中添加class

vue中添加class是一件非常简单的事情：

你可以通过传入一个对象：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17553521540008kuyud.png)

你也可以传入一个数组： 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1755352164000s2273a.png)

甚至是对象和数组混合使用：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17553521710001tnama.png)

# 二、React中添加class

React在JSX给了我们开发者足够多的灵活性，你可以像编写JavaScript代码一样，通过一些逻辑来决定是否添加某些class：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/175535219100040nfiy.png)

这个时候我们可以借助于一个第三方的库：classnames

```bash
npm install classnames
```

很明显，这是一个用于动态添加classnames的一个库。

该`classNames`函数接受任意数量的参数，可以是字符串或对象。参数`'foo'`是 的缩写`{ foo: true }`。如果与给定键关联的值为 false，则该键将不会包含在输出中。

```js
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'

// lots of arguments of various types
classNames('foo', { bar: true, duck: false }, 'baz', { quux: true }); // => 'foo bar baz quux'

// other falsy values are just ignored
classNames(null, false, 'bar', undefined, 0, { baz: null }, ''); // => 'bar'
```

数组将按照上述规则递归展平：

```js
const arr = ['b', { c: true, d: false }];
classNames('a', arr); // => 'a b c'
```

 ES2015 的动态类名：在ES2015 和 Babel 中可用，则可以使用**动态类名**：

```js
const buttonType = 'primary';
classNames({ [`btn-${buttonType}`]: true });
```

