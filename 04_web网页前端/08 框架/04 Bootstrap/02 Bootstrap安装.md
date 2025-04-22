# 一、Bootstrap4的安装
Bootstrap 是一个前端框架。

* 该框架主要是由css和Js组成，但是也会依赖一小部分的HTML。
* 因此在安装Bootstrap时，我们**需要引入相应的CSS和JS文件，当然也需要添加一些全局的配置。**
* 在**Bootstrap 5 版本以前，Bootstrap是依赖jQuery的。**
* 那么如果使用的是Bootstrap5以下的版本，需在**引入Bootstrap之前先引入jQuery库。**

下面我们来看看Bootstrap 安装方式有哪些?

* 方式一:在页面中，直接通过CDN的方式引入。
* 方式二:下载Bootstrap框架，并在页面中手动引入。
* 方式三:使用npm包管理工具安装到项目中(npm在Node基础阶段会讲解)

# 二、方式一：CDN
Bootstrap框架的CDN地址

* https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/css/bootstrap.min.css
* https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js
* https://cdn.jsdelivr.net/npm/bootstrap@4.6.1/dist/js/bootstrap.bundle.min.js

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17419522840003t1k93.png)

**HTML中引入之后，添加重要的全局配置**

* HTML5 文档类型(**doctype或 DOCTYPE**)，Bootstrap要求文档类型(doctype)是HTML5.
	* 如果没有设置这个，就会看到一些古怪的、不完整的样式，因此，正确设置文档类型(doctype)能轻松避免这些困扰。

```html
<!DOCTYPE html>
```

* 添加视口(viewport)
	* Bootstrap 采用的是移动设备优先(mobile first)的开发策略，为了网页能够适配移动端的设备，需在 `<head>`标签中添加**viewport(视口)**
* 在移动端会把 layout viewport 的宽度设置为设备的宽，并且不允许用户进行页面的缩放。

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no,maximum-scale=1.0,minimum-scale=1.0,shrink-to-fit=no">
```

> [!tip] 特别注意
当引入了 Bootstrap 框架以后，CSS文件的 box-size的属性值都设置为border-box。[[12 CSS的盒子模型（Box Model）#十一、CSS属性 box-sizing|box-sizing属性]]

# 三、方式二：下载源码
Bootstrap框架的下载

* Bootstrap下载地址:https://v4.bootcss.com/docs/getting-started/download
* jQuery下载地址:https://jquery.com/download/

忝加重要的全局配置

* HTML5 文档类型(doctype 或 DOCTYPE)Bootstrap 要求文档类型(doctype)是HTML5。
* 添加视口**viewport**(shrink-to-fit 是为了兼容 Safari9 以后版本，禁止页面的伸缩)
* **integrity**:防止资源被篡改，篡改了将不加载;crossorigin:加载不同源的资源时，是否需要需带用户凭证(cookie，证书)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741953549000pgtwy4.png)

# 四、Bootstrap软件包内容
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741953740000xvuuxk.png)


# 五、方式三：npm安装
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1741954057000hh9xpx.png)


![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17419540600000c8x4w.png)



