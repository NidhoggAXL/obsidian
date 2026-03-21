# 一、单页应用程序（SPA）

单页应用程序 (SPA) 全称是：Single-page application，SPA应用是在客户端呈现的（术语称：CRS）。

 - SPA应用默认只返回一个空HTML页面，如：body只有`<div id=“app”></div>`。
 - 而整个应用程序的内容都是通过 Javascript 动态加载，包括应用程序的逻辑、UI 以及与服务器通信相关的所有数据。
 - 构建 SPA 应用常见的库和框架有： React、AngularJS、Vue.js 等。

客户端渲染原理

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773734567000bwz32i.png)


# 二、SPA优缺点

SPA的优点

 - 只需加载一次
	 - SPA应用程序只需要在第一次请求时加载页面，页面切换不需重新加载，而传统的Web应用程序必须在每次请求时都得加载页面，需要花费更多时间。因此，SPA页面加载速度要比传统 Web 应用程序更快。
 - 更好的用户体验
	 - SPA 提供类似于桌面或移动应用程序的体验。用户切换页面不必重新加载新页面
	 - 切换页面只是内容发生了变化，页面并没有重新加载，从而使体验变得更加流畅
 - 可轻松的构建功能丰富的Web应用程序

SPA的缺点

 - SPA应用默认只返回一个空HTML页面，不利于SEO （search engine optimization )
 - 首屏加载的资源过大时，一样会影响首屏的渲染
 - 也不利于构建复杂的项目，复杂 Web 应用程序的大文件可能变得难以维护

# 三、爬虫-工作流程

Google 爬虫的工作流程分为 3 个阶段，并非每个网页都会经历这 3 个阶段：
 - 抓取：
	 - 爬虫（也称蜘蛛），从互联网上发现各类网页，网页中的外部连接也会被发现。
	 - 抓取数以十亿被发现网页的内容，如：文本、图片和视频
 - 索引编制：
	 - 爬虫程序会分析网页上的文本、图片和视频文件
	 - 并将信息存储在大型数据库（索引区）中。
	 - 例如 `<title>` 元素和 Alt 属性、图片、视频等
	 - 爬虫会对内容类似的网页归类分组
	 - 不符合规则内容和网站会被清理
		 - 如：禁止访问 或 需要权限网站等等
 - 呈现搜索结果：当用户在 Google 中搜索时，搜索引擎会根据内容的类型，选择一组网页中最具代表性的网页进行呈现

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773734699000dbmyjr.png)


# 四、搜索引擎的优化（SEO）

语义性HTML标记

 - 标题用`<h1>`，一个页面只有一个； 副标题用`<h2>`到`<h6>`。
 - 不要过度使用h标签，多次使用不会增加 SEO（search engine optimization )。
 - 段落用`<p>`，列表用`<ul>`，并且li只放在 ul 中 等等。

每个页面需包含：标题 + 内部链接
 - 每个页面对应的title，同一网站所有页面都有内链可以指向首页

确保链接可供抓取，如图所示：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177373542700050214b.png)


meta标签优化：设置 description keywords 等

文本标记和img：
 - 比如`<b>`和`<strong>`加粗文本的标签，爬虫也会关注到该内容
 - img标签添加 alt 属，图片加载失败，爬虫会取alt内容。

robots.txt 文件：规定爬虫可访问您网站上的哪些网址。

sitemap.xml站点地图：在站点地图列出所有网页，确保爬虫不会漏掉某些网页

更多查看：https://developers.google.com/search/docs/crawling-indexing/valid-page-metadata

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773735433000mizgzx.png)

# 五、静态站点生成(SSG)

静态站点生成(SSG) 全称是：Static Site Generate，是预先生成好的静态网站。

 - SSG 应用一般在构建阶段就确定了网站的内容。
 - 如果网站的内容需要更新了，那必须得重新再次构建和部署。
 - 构建 SSG 应用常见的库和框架有： Vue Nuxt、 React Next.js 等。

SSG的优点：

 - 访问速度非常快，因为每个页面都是在构建阶段就已经提前生成好了。
 - 直接给浏览器返回静态的HTML，**也有利于SEO**
 - SSG应用依然保留了SPA应用的特性，比如：前端路由、响应式数据、虚拟DOM等

SSG的缺点：

 - 页面都是静态，**不利于展示实时性的内容**，**实时性的更适合SSR**。
 - 如果站点内容更新了，那必须得**重新再次构建和部署**。

# 六、服务器端渲染（SSR）

服务器端渲染全称是：Server Side Render，在服务器端渲染页面，并将渲染好HTML返回给浏览器呈现。

 - SSR应用的页面是在服务端渲染的，用户每请求一个SSR页面都会先在服务端进行渲染，然后将渲染好的页面，返回给浏览器
呈现。
 - 构建 SSR 应用常见的库和框架有： Vue Nuxt、 React Next.js 等（SSR应用也称同构应用） 。

服务器端渲染流程：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773736252000576wfe.png)

服务器端渲染原理

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773736867000re04w5.png)

# 七、SSR优缺点

SSR的优点

 - **更快的首屏渲染速度**
	 - 浏览器显示静态页面的内容要比 JavaScript 动态生成的内容快得多。
	 - 当用户访问首页时可立即返回静态页面内容，而不需要等待浏览器先加载完整个应用程序。
 - **更好的SEO**
	 - 爬虫是最擅长爬取静态的HTML页面，服务器端直接返回一个静态的HTML给浏览器。
	 - 这样有利于爬虫快速抓取网页内容，并编入索引，有利于SEO。
 - SSR应用程序在 Hydration 之后依然可以**保留 Web 应用程序的交互性**。比如：前端路由、响应式数据、虚拟DOM等。

SSR的缺点

 - SSR 通常需要对服务器进行更多 API 调用，以及在服务器端渲染需要消耗更多的服务器资源，**成本高**。
 - **增加了一定的开发成本**，用户需要关心哪些代码是运行在服务器端，哪些代码是运行在浏览器端。
 - SSR 配置站点的**缓存**通常会比SPA站点要**复杂一点**。

# 八、SSR 解决方案

SSR的解决方案：

 - 方案一：php、jsp ...
 - 方案二：从零搭建 SSR 项目（ Node+webpack+Vue/React ）
 - 方案三：直接使用流行的框架（推荐）
	 - React : Next.js
	 - Vue3 : Nuxt3 | | Vue2 : Nuxt.js
	 - Angular : Anglular Universal

SSR应用场景非常广阔，比如：

 - SaaS产品，如：电子邮件网站、在线游戏、客户关系管理系统（CRM）、采购系统等
 - 门户网站、电子商务、零售网站
 - 单个页面、静态网站、文档类网站
 - 等等

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17737370510006vx8pk.png)


