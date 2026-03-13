# 一、bable-loader案例

我们知道babel-loader可以帮助我们对JavaScript的代码进行转换，这里我们定义一个自己的babel-loader：

需要使用到 @babel/core 来解析代码，但是通过调用自己的loader：

```shell
npm install @babel/core -D
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773406029000fnnht1.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773406040000pnmnbx.png)


# 二、解析md文档

解析md文档需要使用到一个库：marked

```shell
npm installl marked -D
```

为了方便把解析后的md文档显示到页面，需要使用到 [[03 Html-Webpack-Plugin|Html-Webpack-Plugin]] 来打包出一个 html 。

```shell
npm install html-webpack-plugin -D
```

md的文档：

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773408230000bv3l5g.png)


xlmd-loader的编写：

```js
// xlmd-loader.js
const { marked } = require("marked")
module.exports = function (content) {
  // console.log("---", content)

  // 将md转换为html
  const htmlContent = marked(content)

  // 转换为模块化
  const innerContent = "`" + htmlContent + "`"
  const moduleCode = `var code=${innerContent}; export default code;`

  // 返回的结果必须是模块化内容
  return moduleCode
}
```

webpack的配置：

![gh|600](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773408285000hjugtr.png)

入口文件：

```js
import code from "./md/learn.md"
const message = "hello"
console.log(message)

const foo = () => {
  console.log("foo function")
}

// 将code显示到页面
document.body.innerHTML = code
```

结果显示：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17734083590007kih0s.png)

但是这样显示的代码块没有一些对应的高亮并不是很好看，那么就可以使用一个给代码关键字提供高亮的关键字 highlight.js 的库和这个库对应的 markedHighlight 插件

```shell
npm install highlight.js marked-highlight -D
```

loader代码：

```js
const { marked } = require("marked");
const hljs = require("highlight.js");
const { markedHighlight } = require("marked-highlight");

module.exports = function (content) {
  /**
   * 使用marked库的插件功能，配置代码高亮
   * 使用markedHighlight插件，结合highlight.js实现代码语法高亮
   */
  marked.use(
    //  配置markedHighlight插件
    markedHighlight({
      //  高亮处理函数code(代码)和lang(语言)
      highlight(code, lang) {
        //  检查是否支持指定的语言，不支持则默认使用纯文本格式
        const language = hljs.getLanguage(lang) ? lang : "plaintext";
        //  使用highlight.js对代码进行高亮处理
        return hljs.highlight(code, { language }).value;
      },
    }),
  );

  // 将md转换为html
  const htmlContent = marked(content);

  // 转换为模块化
  const innerContent = "`" + htmlContent + "`";
  const moduleCode = `var code=${innerContent}; export default code;`;

  // 返回的结果必须是模块化内容
  return moduleCode;
};

```


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773411057000kwtiqq.png)

这样关键字就可以标识出来，可以使用选择器对这些关键字进行自我的样式编写，同时也可以使用 highlight.js 默认的样式，在入口文件导入。

```js
import code from "./md/learn.md"
import "highlight.js/styles/github.css";//highlight.js默认样式

const message = "hello"
console.log(message)

const foo = () => {
  console.log("foo function")
}

// 将code显示到页面
document.body.innerHTML = code
```

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773411179000odv594.png)
