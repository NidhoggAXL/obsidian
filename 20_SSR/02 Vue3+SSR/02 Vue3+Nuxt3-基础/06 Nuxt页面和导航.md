# 一、新建页面

Nuxt项目中的页面是在 app/pages 目录下创建的

在pages目录创建的页面，Nuxt会根据该页面的目录结构和其文件名来自动生成对应的路由。

页面路由也称为文件系统路由system器（file  router），路由是Nuxt的核心功能之一

新建页面步骤

 - 1.创建页面文件，比如： pages/index.vue
 - 2.将<NuxtPage /> 内置组件添加到 app.vue
 - 3. app.vue 页面会自动使用 pages/index.vue 替换占位符
 - 4. 如果是在 pages 下面再次创建问价夹，文件 app/pages/about/index.vue 也可以自动替换
	 - **如果是在 about/about.vue 这样的话，路由跳转路径就不可以编写为 `/about` 而是为 `/about/about`**


命令快速创建页面

 - `npx nuxi add page home` # 创建home页面
 - `npx nuxi add page detail/[id]` # 创建detail页面
 - `npx nuxi add page user-[role]/[id]` # 创建user页面

# 二、组件导航

`<NuxtLink>`是Nuxt内置组件，**是对 RouterLink 的封装**，用来实现页面的导航。

 - 该组件底层是一个`<a>`标签，因此使用 a + href 属性也支持路由导航
 - 但是用a标签导航会有触发浏览器默认刷新事件，而 NuxtLink 不会，NuxtLink还扩展了其它的属性和功能

**应用Hydration后（已激活，可交互），页面导航会通过前端路由来实现。这可以防止整页刷新**

当然，手动输入URL后，点击刷新浏览器也可导航，这会导致整个页面刷新

NuxtLink 组件属性：

 - to：支持路由路径、路由对象、URL
 - href：to的别名
 - activeClass：激活链接的类名
 - target：和a标签的target一样，指定何种方式显示新页面
 - repalce：是否替换当前页面，前一个路由页面回退就不会到
 - 等等

当然也可以添加传递查询参数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17739232660004phv3b.png)

# 三、编程导航

## 3.1 navigateTo

Nuxt除了可以通过`<NuxtLink>`内置组件来实现导航，同时也支持编程导航：navigateTo 。

通过编程导航，在应用程序中就可以轻松实现动态导航了，但是编程导航不利于SEO。

navigateTo 函数在服务器端和客户端都可用，也可以在插件、中间件中使用，也可以直接调用以执行页面导航，例如：

 - 当用户触发该goToProfile()方法时，我们通过navigateTo函数来实现动态导航。
 - 建议： goToProfile方法总是返回 navigateTo 函数（该函数不需要导入）或 **返回异步函数**

navigateTo( to , options) 函数:

 - to: 可以是纯字符串 或 外部URL 或 路由对象，如右图所示：
 - options: 导航配置，可选
	 - replace：默认为false，为true时会替换当前路由页面
	 - external：默认为false，不允许导航到外部连接，true则允许
	 - 等等

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773923964000r12jxi.png)

## 3.2 useRouter

Nuxt中的编程导航除了可以通过 navigateTo 来实现导航，同时也支持 useRouter ( 或 Options API 的 this.$router )

useRouter常用的API

 - back：页面返回，和 一样 router.go(-1)
 - forward：页面前进，同 router.go(1)
 - go：页面返回或前进，如 router.go(-1) or router.go(1)
 - push：以编程方式导航到新页面。建议改用 navigateTo 。支持性更好
 - replace：以编程方式导航到新页面，但会替换当前路由。建议改用 navigateTo 。支持性更好
 - beforeEach：路由守卫钩子，每次导航前执行（用于全局监听）
 - afterEach：路由守卫钩子，每次导航后执行（用于全局监听）
 - .....

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773924317000cgi1gl.png)


# 四、动态路由

Nuxt3 和 Vue一样，也是支持动态路由的，只不过在Nuxt3中，动态路由也是根据目录结构和文件的名称自动生成。

动态路由语法：

 - 页面组件目录 或 页面组件文件都 支持 `[ ]` 方括号语法
 - 方括号里编写动态路由的参数。

例如，动态路由 支持如下写法：

 - `pages/detail/[id].vue -> /detail/:id`
 - `pages/detail/user-[id].vue -> /detail/user-:id`
 - `pages/detail/[role]/[id].vue -> /detail/:role/:id`
 - `pages/detail-[role]/[id].vue -> /detail-:role/:id`

# 五、路由参数

动态路由参数

 - 通过 `[]` 方括号语法定义动态路由，比如：`/detail/[id].vue`
 - 页面跳转时，在URL路径中传递动态路由参数，比如：`/detail/10010`
 - 目标页面通过 **route.params** 获取动态路由参数

查询字符串参数

 - 页面跳转时，通过查询字符串方式传递参数，比如：`/detail/10010?name=liujun`
 - 目标页面通过 **route.query** 获取查询字符串参数

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773993431000n07fif.png)

# 六、通配路由

捕获所有不配路由（即 404 not found 页面）

 - 通过在方括号内添加三个点 ，如：`[...slug].vue` 语法，其中slug可以是其它字符串。
 - 除了支持在 pages根目录下创建，也支持在其子目录中创建。

# 七、路由匹配规则

预定义路由优先于动态路由，动态路由优先于捕获所有路由。请看以下示例：

1.预定义路由：pages/detail/create.vue

 - 将匹配 /detail/create

2.动态路由：`pages/detail/[id].vue`

 - 将匹配/detail/1, /detail/abc 等。
 - 但不匹配 /detail/create 、/detail/1/1、/detail/ 等

3.捕获所有路由：`pages/detail/[...slug].vue`

 - 将匹配 /detail/1/2, /detail/a/b/c 等。
 - 但不匹配 /detail 等

# 八、嵌套路由

Nuxt 和 Vue一样，也是支持嵌套路由的，只不过在Nuxt中，**嵌套路由也是根据目录结构和文件的名称自动生成。**

编写嵌套路由步骤：

 - 1.创建一个一级路由，如：parent.vue
 - 2.创建一个与一级路由同名同级的文件夹，如： parent
 - 3.在parent文件夹下，创建一个嵌套的二级路由
	 - 如：parent/child.vue， 则为一个二级路由页面
	 - 如： parent/index.vue 则为二级路由默认的页面
 - 4.需要在parent.vue中添加 NuxtPage 路由占位

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17739963090007u56yn.png)

# 九、路由中间件

Nuxt 提供了一个可定制的 路由中间件，用来监听路由的导航，包括：局部和全局监听（支持再服务器和客户端执行）

路由中间件分为三种：

匿名（或内联）路由中间件：在页面中使用 definePageMeta 函数定义，可监听局部路由。当注册多个中间件时，会按照注册顺序来执行。

![gh|500](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774010758000kdnf6c.png)

命名路由中间件：在 middleware 目录下定义，并会自动加载中间件。命名规范 kebab-case）

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177401102300088c8zi.png)


全局路由中间件（优先级比前面的高，支持两端）：在 middleware 目录中，需带.global后缀的文件，每次路由更改都会自动运行。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177401123100086h0s8.png)

# 十、路由验证( validate )

Nuxt支持对每个页面路由进行验证，我们可以通过 **definePageMeta** 中的 **validate属性** 来对路由进行验证。

 - validate属性接受一个回调函数，回调函数中以 route 作为参数
 - 回调函数的返回值支持：
	 - 返回 bool 值来确定是否放行路由
	 - true 放行路由
	 - false 默认重定向到内置的 404 页面
 - 返回对象 ： `{ status:404 }` // 返回自定义的 401 页面，验证失败

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774014762000hvsino.png)


路由验证失败，可以自定义错误页面：在项目根目录（**不是pages目录**）新建 error.vue

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774014871000ebs92l.png)

