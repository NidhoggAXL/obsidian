# 一、认识Vue插件

通常向Vue全局添加一些功能时，会采用插件的模式，它有两种编写方式:

- **对象类型**：一个对象，但是必须<mark class="hltr-cyan">包含一个 install 的函数</mark>，该函数会在安装插件时执行;
- **函数类型**：一个function，这个函数会在安装插件时<mark class="hltr-cyan">自动执行函数类型</mark>:

插件可以完成的功能没有限制，比如下面的几种都是可以的:

- 添加全局方法或者 property，通过把它们<mark class="hltr-cyan">添加到 config.globalProperties 上实现</mark>;
- 添加全局资源：指令/过滤器/过渡等
- 通过全局 mixin 来添加一些组件选项
- 一个库，提供自己的 API，同时提供上面提到的一个或多个功能

> [!tip]
> 
> Vue安装插件的本质是会在使用插件的时候，把 reateApp 创建的对象在使用 use 的时候，会把本身作为参数闯入进去，
> 
> 例如： `const app = createApp(App)` 后面 `app.use()` 安装插件的时候，会把 app 作为参数传入插件的对象的install方法和插件函数里面。


# 二、插件的编写方式


对象类型的写法：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753407681000ciearc.png)

函数类型的写法：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753407709000tttm2c.png)

使用的时候：

```
app.use(对象) 或者 app.use(函数)
```

# 三、例子

比如前面的自定义指令的封装：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753407844000zyg27y.png)

在使用的时候：

```js
import { createApp } from 'vue'
import App from './01 自定义指令/App.vue'
import useDirectives from './01 自定义指令/directives'

const app = createApp(App)

//1.不使用插件的写法
//useDirectives(app)

//2.使用插件的写法
//app.use(useDirectives)

app.mount('#app')
```


