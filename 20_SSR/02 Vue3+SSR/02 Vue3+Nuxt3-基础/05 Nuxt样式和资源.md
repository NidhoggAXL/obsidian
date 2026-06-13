# 一、全局样式

编写**全局样式**步骤

 - 1.在assets中编写全局样式，比如：globel.scss
 - 2.接着在nuxt.config中的css选项中配置
 - 3.接着执行npm i –D sass 即可

编写样式表最合适的位置是assets目录。 然后可以在app.vue（或布局文件）中使用预处理器的语法导入源文件。

```css
.global-style {
  font-size: 20px;
  color: red;
}
```

```vue
// app.vue
<style lang="scss">
@use "~/assets/scss/main.scss";
</style>

```

或者，你也可以使用Nuxt配置的`css`属性。

```ts
export default defineNuxtConfig({
  css: ['~/assets/scss/main.scss']
})
```

定义**全局变量**步骤 

 - 1.在assets中编写全局样式变量
 - 2.接着在nuxt.config中的vite选项中配置
 - 3.然后就可以在任意组件中或scss文件中直接使用全局变量

```sass
$primary: #49240F;
$secondary: #E4A79D;
```

```ts
// next.config.ts
export default defineNuxtConfig({
  vite: {
    css: {
      preprocessorOptions: {
        scss: {
          // 自动给 scss 模块添加@use "~/assets/_colors.scss" as *
          additionalData: '@use "~/assets/_colors.scss" as *;'
        }
      }
    }
  }
})

```

> [!tip]
> Nuxt默认使用Vite。如果你想使用webpack，请参考每个预处理器加载器的文档。


# 二、资源导入

public目录

 - 用作静态资产的公共服务器，可在应用程序上直接通过 URL 直接访问
 - 比如：引用public/img/ 目录中的图像文件
	 - 在静态 URL 中可用 /img/nuxt.png，如右图
	 - 静态的URL也**支持在背景中使用**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17739146570004joazr.png)

assets目录

 - assets经常用于存放如样式表、字体或 SVG的资产
 - 可以使用 ~/assets/ 路径引用位于assets目录中的资产文件
 - ~/assets/ 路径也支持在背景中使用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773914682000951vvq.png)

# 三、字体图标

字体图标使用步骤

 - 1.将字体图标存放在assets目录下
 - 2.字体文件可以使用 ~/assets/ 路径引用。
 - 3.在nuxt.config配置文件中导入全局样式
 - 4.在页面中就可以使用字体图标了

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773920580000c8rase.png)



