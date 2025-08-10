# 一、认识Vue插件

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17534076510008zzta3.png)


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


