# 一、App生命周期

监听App的生命周期的Hooks: https://nuxt.com.cn/docs/4.x/guide/concepts/nuxt-lifecycle

 - App Hooks 主要可由 **Nuxt 插件** 使用 hooks 来监听 **生命周期**，也可用于 Vue 组合 API  `app/plugins/lifecycle.ts`。
 - 但是，如在**组件中编写hooks来监听**，那 create和setup hooks就监听不了，因为这些hooks已经触发完了监听。
 - https://nuxt.com.cn/docs/4.x/api/advanced/hooks

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774080409000hewnt7.png)

# 二、组件生命周期

客户端生命周期：组合是API -> OptionsAPI

![gh|400](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774083139000mq3szj.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1774083210000ur1z47.png)

服务器端生命周期：

 - OptionsAPI：setup、beforeCreate、created
 - 组合式API：不会执行任何生命周期









