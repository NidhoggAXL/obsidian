# 一、认识tsconfig.json文件

什么是tsconfig.json文件呢？（官方的解释）

- 当目录中出现了 tsconfig.json 文件，则说明该目录是 TypeScript 项目的根目录；
- tsconfig.json 文件指定了编译项目所需的根目录下的文件以及编译选项。


tsconfig.json文件有两个作用：

- **作用一（主要的作用）**：让TypeScript Compiler在编译的时候，知道如何去编译TypeScript代码和进行类型检测；
	- 比如是否允许不明确的this选项，是否允许隐式的any类型；
	-  将TypeScript代码编译成什么版本的JavaScript代码；
- **作用二：让编辑器（比如VSCode）可以按照正确的方式识别TypeScript代码**；
	-  对于哪些语法进行提示、类型错误检测等等；

JavaScript 项目可以使用 jsconfig.json 文件，它的作用与 tsconfig.json 基本相同，只是默认启用了一些 JavaScript 相关的编译选项。

# 二、tsconfig.json配置

tsconfig.json在编译时如何被使用呢?

- 在**调用 tsc 命令并且没有其它输入文件参数**时，编译器**将由当前目录开始向父级目录寻找包含 tsconfig 文件的目录**。
- 调用 tsc 命令并且没有其他输入文件参数，**可以使用 --project （或者只是 -p）的命令行选项来指定包含了 tsconfig.json 的目录**；
- 当**命令行中指定了输入文件参数， tsconfig.json 文件会被忽略**；

webpack中使用ts-loader进行打包时，也会自动读取tsconfig文件，根据配置编译TypeScript代码。

tsconfig.json文件包括哪些选项呢？

- tsconfig.json本身包括的选项非常非常多，我们不需要每一个都记住；
- 可以查看文档对于每个选项的解释：https://www.typescriptlang.org/tsconfig
- 当我们开发项目的时候，选择TypeScript模板时，tsconfig文件默认都会帮助我们配置好的

# 三、tsconfig.json顶层选择

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17607005950006h2emq.png)


# 四、tsconfig.json文件

tsconfig.json是用于配置TypeScript编译时的配置选项：  https://www.typescriptlang.org/tsconfig

# 五、常见的tsconfig.json配置

## 🎯 tsconfig.json 是什么

`tsconfig.json` 是 TypeScript 项目的核心配置文件，通常位于项目根目录。它告诉 TypeScript 编译器如何编译你的项目，例如编译哪些文件、输出到什么目录、使用哪个 ECMAScript 标准等。[](https://developer.aliyun.com/article/1069316)[](https://juejin.cn/post/7549024057036046386)

你可以通过执行 `tsc --init` 命令来快速生成一个包含默认配置的 `tsconfig.json` 文件。[](https://developer.aliyun.com/article/1069316)

## 📦 项目文件管理

这些顶层配置项用于指定编译器需要处理哪些文件。

|配置项|作用描述|示例与备注|
|---|---|---|
|`include`|指定要编译的文件或模式。|`["src/**/*"]` 表示编译 `src` 目录下的所有文件。[](https://developer.aliyun.com/article/1069316)[](https://www.nowcoder.com/discuss/513481273562750976)|
|`exclude`|指定编译时需要排除的文件或模式。**它只影响 `include`**。[](https://juejin.cn/post/7549024057036046386)|通常排除 `node_modules`、`dist`、测试文件等。[](https://developer.aliyun.com/article/1069316)[](http://t.zoukankan.com/mengfangui-p-12263071.html)|
|`files`|明确列出需要编译的少量文件。|适合文件极少的项目，不能使用通配符。[](https://www.nowcoder.com/discuss/513481273562750976)|
|`extends`|**继承**另一个 tsconfig 文件的配置。|`"extends": "./base.json"`，这对于统一 Monorepo 中多个包的配置非常有用。[](https://juejin.cn/post/7549024057036046386)[](https://zhuanlan.zhihu.com/p/570939192)|
|`references`|配置**项目引用**，用于将大型项目拆分成相互依赖的多个子项目。[](https://juejin.cn/post/7549024057036046386)|需要子项目在 `compilerOptions` 中开启 `composite: true`。[](https://juejin.cn/post/7549024057036046386)|

## ⚙️ 编译器核心选项 (compilerOptions)

`compilerOptions` 是配置的核心，控制了代码转换和类型检查的具体规则。

### 目标与模块

|配置项|作用描述|常见取值|
|---|---|---|
|`target`|指定编译后代码的 **ECMAScript 目标版本**。[](https://developer.aliyun.com/article/1069316)[](https://www.nowcoder.com/discuss/513481273562750976)|`"es5"`（兼容性好），`"es2015"`（ES6），`"esnext"`（最新）。[](https://developer.aliyun.com/article/1069316)[](https://zhuanlan.zhihu.com/p/570939192)|
|`module`|指定生成代码的**模块系统**。[](https://developer.aliyun.com/article/1069316)[](https://www.nowcoder.com/discuss/513481273562750976)|`"commonjs"`（Node.js），`"es2015"`（ES 模块）。[](https://developer.aliyun.com/article/1069316)[](http://t.zoukankan.com/mengfangui-p-12263071.html)|
|`lib`|指定编译器要包含的**内置 API 类型声明**。[](https://developer.aliyun.com/article/1069316)[](http://t.zoukankan.com/Leophen-p-14959214.html)|`["es2015", "dom"]` 引入 ES2015 和 DOM 的类型。[](https://www.nowcoder.com/discuss/513481273562750976)[](http://t.zoukankan.com/Leophen-p-14959214.html)|
|`moduleResolution`|指定**模块解析策略**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](http://t.zoukankan.com/Leophen-p-14959214.html)|`"node"`（常用），`"classic"`。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](http://t.zoukankan.com/Leophen-p-14959214.html)|

### 输出与控制

|配置项|作用描述|
|---|---|
|`outDir`|指定编译后的 **JavaScript 文件输出目录**。[](https://developer.aliyun.com/article/1069316)[](http://t.zoukankan.com/mengfangui-p-12263071.html)|
|`rootDir`|指定源代码的**根目录**，编译器输出的目录结构会与此对应。[](https://developer.aliyun.com/article/1069316)[](https://www.nowcoder.com/discuss/513481273562750976)|
|`removeComments`|编译时**删除注释**以减小文件体积。[](https://developer.aliyun.com/article/1069316)[](https://www.nowcoder.com/discuss/513481273562750976)|
|`sourceMap`|是否生成 **Source Map 文件**，便于调试。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://developer.aliyun.com/article/1069316)|
|`noEmit`|**只进行类型检查，不输出**任何文件。[](https://developer.aliyun.com/article/1069316)[](https://www.nowcoder.com/discuss/513481273562750976)|

### 语法兼容与互操作

|配置项|作用描述|
|---|---|
|`allowJs`|**允许编译 JavaScript 文件**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://developer.aliyun.com/article/1069316)|
|`checkJs`|在 JavaScript 文件中**报告错误**，通常与 `allowJs` 一起使用。[](https://developer.aliyun.com/article/1069316)[](http://t.zoukankan.com/Leophen-p-14959214.html)|
|`jsx`|控制如何处理 **`.tsx` 文件中的 JSX 语法**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://www.nowcoder.com/discuss/513481273562750976)|
|`esModuleInterop`|为了更好地与 **CommonJS 模块互操作**，允许默认导入。**建议开启**。[](https://developer.aliyun.com/article/1069316)[](https://zhuanlan.zhihu.com/p/570939192)|
|`resolveJsonModule`|**允许导入 JSON 模块**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://www.nowcoder.com/discuss/513481273562750976)|
|`experimentalDecorators`|启用**实验性的装饰器**语法支持。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://www.nowcoder.com/discuss/513481273562750976)|

## 🔍 类型检查与严格模式

开启严格模式是保证代码质量、减少运行时错误的最佳实践。[](https://zhuanlan.zhihu.com/p/570939192) 你可以使用 `"strict": true` 一键开启所有严格检查选项。[](https://juejin.cn/post/7549024057036046386)[](https://www.nowcoder.com/discuss/513481273562750976)

下表是 `strict` 开启后，一些关键的子选项及其作用：

|配置项|作用描述|
|---|---|
|`noImplicitAny`|**禁止隐式的 `any` 类型**。要求为变量和参数显式指定类型。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`strictNullChecks`|**启用严格的 `null` 和 `undefined` 检查**。防止意外地将它们赋值给其他类型。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://developer.aliyun.com/article/1069316)|
|`strictFunctionTypes`|对函数类型进行**严格的协变和逆变检查**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`strictBindCallApply`|确保 `bind`、`call`、`apply` 方法的参数类型与原函数匹配。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`strictPropertyInitialization`|确保**类的实例属性在构造函数中初始化**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`noImplicitThis`|禁止 **`this` 表达式有隐式的 `any` 类型**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`useUnknownInCatchVariables`|将 `catch` 子句的异常变量类型设为 **`unknown` 而非 `any`**，强制类型检查。[](https://juejin.cn/post/7549024057036046386)|

### 其他有用的检查选项

这些选项不直接包含在 `strict` 中，但非常实用：

|配置项|作用描述|
|---|---|
|`noUnusedLocals`|报告**未使用的局部变量**的错误。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`noUnusedParameters`|报告**未使用的函数参数**的错误。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`noImplicitReturns`|检查函数**所有路径是否都有返回值**。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
|`noFallthroughCasesInSwitch`|报告 **`switch` 语句中 case 贯穿**的错误。[](https://www.npmjs.com/package/@aurorafe/tsconfig/v/1.0.1?activeTab=readme)[](https://juejin.cn/post/7549024057036046386)|
## 💻 实用配置示例

### 1. React Native 项目

根据 React Native 官方文档，配置可以非常简洁：

```JSON
{
  "extends": "@react-native/typescript-config"
}
```

### 2. 一个通用的现代前端项目配置

```JSON
{
  "compilerOptions": {
    "target": "es5",
    "module": "esnext",
    "lib": ["dom", "esnext"],
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "resolveJsonModule": true,
    "jsx": "react-jsx"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

## 💎 总结与建议

- **从 `strict: true` 开始**：虽然开始时可能会需要多写一些类型代码，但它能从根源上避免许多潜在错误，从长远看利远大于弊。
    
- **善用 `extends`**：很多框架（如 React Native）或团队有预设配置，直接继承可以保持规范统一并减少配置成本。
    
- **理解 `target` 和 `lib`**：根据你的项目需要运行的平台（如老旧浏览器还是现代 Node.js）来设置这两个选项。

