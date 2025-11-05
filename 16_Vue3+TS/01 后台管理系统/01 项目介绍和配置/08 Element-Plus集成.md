# 一、集成方案

Element Plus UI组件库

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1761803826000k0oobr.png)

集成方案： 

- 安装：https://element-plus.gitee.io/zh-CN/guide/installation.html 
- 导入：https://element-plus.gitee.io/zh-CN/guide/quickstart.html

# 二、按需引入TS配置

下载插件：

```bash
npm install -D unplugin-vue-components unplugin-auto-import
```

配置 Vite (vite.config.ts)

```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    vue(),
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```


在按需引入的时候，TS的提示不是很好，要进行配置：把那两个插件放入到 TS 检测的文件中。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1761803919000sioite.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17618039690000brt02.png)

# 三、Icons的集成

Element-Plus的Icon组件文档中有这么一句话[说明](https://element-plus.org/zh-CN/component/icon)：如果你想像用例一样**直接使用**，你需要<mark class="hltr-cyan">全局注册组件</mark>，才能够直接在项目里使用。

在使用Element-Plus库的Icon组件的时候，如果要和它的例子一样使用 Icon 组件的话，必须全局注册，按需引入的话会有问题。

## 3.1 全局注册

为了代码的逻辑性强，会在 src 下面创建一个 global 文件，里面存放 `regitser-icons.ts` 文件，在里面编写[[04 Vue中安装插件的方式|Vue的插件]]：

```ts
import type { App } from 'vue'
import * as ElementPlusIconsVue from "@element-plus/icons-vue"

function RefisterIcons(app: App<Element>) {
  for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
    app.component(key, component)
  }
}

export default RefisterIcons

```

再在 main.ts 文件里面使用插件：

```ts
import { createApp } from "vue"
//引入自定义插件
import RegisterIcons from '@/global/register-icons'

import "normalize.css"
import "./styles/index.less"

import router from "./router/index"
import pinia from "./stores"

import App from "./App.vue"

createApp(App).use(router).use(pinia).use(RegisterIcons).mount("#app")

```


## 3.2 动态Icons

在使用动态的 Icons 的时候，都是根据服务器返回的数据来确定要使用那一个 icon 的，这样就可以根据服务器返回的数据确定不同的 icon。

要使用到 [[03 动态组件的使用|Vue的动态组件]] ，根据服务器返回不同的字符串进行选择不同的 icon。

```html
<!-- 服务器类似放回 el-icon-location 的字符串 -->
<el-icon>
  <component :is="item.icon.split('-icon-')[1]" />
</el-icon>
```



# 四、FormInstance获取表单实例

**FormInstance 详细说明**：`FormInstance` 是 Element Plus 为表单组件提供的**类型接口**，它专门定义了表单实例的**公共 API 方法**，而不包含内部实现细节

## FormInstance 的核心定义

```ts
// Element Plus 内部的实际定义（简化版）
interface FormInstance {
  // 表单验证方法
  validate: (callback?: (valid: boolean, fields?: ValidateFieldsError) => void) => Promise<void>
  validateField: (props?: Arrayable<FormItemProp>, callback?: (errorMessage: string) => void) => void
  clearValidate: (props?: Arrayable<FormItemProp>) => void
  resetFields: (props?: Arrayable<FormItemProp>) => void
  
  // 表单状态相关
  scrollToField: (prop: FormItemProp) => void
  updateDomain: () => void
  
  // 内部方法（通常不需要直接使用）
  // ... 其他内部方法
}
```

## 🎯 为什么使用 FormInstance

### 1. **类型安全且精确**

```ts
import type { FormInstance } from 'element-plus'

const formRef = ref<FormInstance>()

// ✅ 只能访问定义好的公共方法
formRef.value?.validate((valid) => { /* ... */ })
formRef.value?.resetFields()

// ❌ 无法访问内部私有属性和方法
// formRef.value?.$el // 类型错误
// formRef.value?.validate // 正确，因为这是公共API
```

### 2. **避免实现细节耦合**

```ts
// 使用 InstanceType<typeof ElForm> - 可能访问到内部实现
const formRef = ref<InstanceType<typeof ElForm>>()
// 可能意外触发内部状态变化，影响样式和行为

// 使用 FormInstance - 只关注公共契约
const formRef = ref<FormInstance>()
// 只使用稳定的公共API，不会影响内部状态
```

## 🔧 完整的使用示例

```ts
<script setup lang="ts">
import type { FormInstance, FormRules } from 'element-plus'
import { reactive, ref } from 'vue'

const formRef = ref<FormInstance>()

const formData = reactive({
  username: '',
  password: '',
  email: ''
})

const rules: FormRules = {
  username: [
    { required: true, message: '请输入用户名', trigger: 'blur' },
    { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' }
  ],
  email: [
    { type: 'email', message: '请输入正确的邮箱地址', trigger: 'blur' }
  ]
}

// 1. 完整表单验证
const validateForm = async () => {
  try {
    await formRef.value?.validate()
    console.log('验证成功')
  } catch (error) {
    console.log('验证失败', error)
  }
}

// 2. 验证特定字段
const validateUsername = () => {
  formRef.value?.validateField('username', (errorMessage) => {
    console.log('用户名验证结果:', errorMessage)
  })
}

// 3. 重置表单
const resetForm = () => {
  formRef.value?.resetFields()
}

// 4. 清除验证
const clearValidation = () => {
  formRef.value?.clearValidate()
  // 或者清除特定字段的验证
  formRef.value?.clearValidate(['username', 'email'])
}
</script>

<template>
  <el-form
    ref="formRef"
    :model="formData"
    :rules="rules"
    label-width="100px"
  >
    <el-form-item label="用户名" prop="username">
      <el-input v-model="formData.username" />
    </el-form-item>
    
    <el-form-item label="密码" prop="password">
      <el-input v-model="formData.password" type="password" />
    </el-form-item>
    
    <el-form-item label="邮箱" prop="email">
      <el-input v-model="formData.email" />
    </el-form-item>
    
    <el-form-item>
      <el-button @click="validateForm">验证表单</el-button>
      <el-button @click="resetForm">重置</el-button>
      <el-button @click="clearValidation">清除验证</el-button>
    </el-form-item>
  </el-form>
</template>
```

## 🔍 FormInstance 的方法详解

### 1. **validate()** - 完整表单验证

```ts
// 回调函数方式
formRef.value?.validate((valid, fields) => {
  if (valid) {
    console.log('验证成功')
  } else {
    console.log('验证失败', fields)
  }
})

// Promise 方式（推荐）
try {
  await formRef.value?.validate()
  console.log('验证成功')
} catch (error) {
  console.log('验证失败', error)
}
```

### 2. **validateField()** - 验证特定字段

```ts
// 验证单个字段
formRef.value?.validateField('username', (errorMessage) => {
  if (errorMessage) {
    console.log('验证失败:', errorMessage)
  } else {
    console.log('验证成功')
  }
})

// 验证多个字段
formRef.value?.validateField(['username', 'email'])
```

### 3. **resetFields()** - 重置表单

```ts
// 重置所有字段
formRef.value?.resetFields()

// 重置特定字段
formRef.value?.resetFields(['username', 'email'])
```

### 4. **clearValidate()** - 清除验证状态

```ts
// 清除所有验证
formRef.value?.clearValidate()

// 清除特定字段验证
formRef.value?.clearValidate('username')
formRef.value?.clearValidate(['username', 'email'])
```

## 🆚 与 `InstanceType<typeof ElForm>` 的对比

|特性|FormInstance|InstanceType<typeof ElForm>|
|---|---|---|
|**类型范围**|仅公共API方法|完整组件实例（公共+私有）|
|**类型安全**|✅ 高，只暴露稳定接口|❌ 低，可能访问到内部实现|
|**维护性**|✅ 高，接口稳定|❌ 低，依赖内部实现|
|**样式影响**|✅ 无副作用|❌ 可能影响内部状态和样式|
|**使用场景**|表单操作和验证|需要访问组件内部细节|

## 💡 最佳实践建议

1. **常规使用**：总是优先使用 `FormInstance`
    
2. **特殊情况**：只有在需要访问 Element Plus 内部未暴露的功能时才考虑 `InstanceType`
    
3. **类型导入**：使用 `import type` 避免运行时依赖
    
4. **可选链**：总是使用可选链操作符安全访问方法

```ts
// ✅ 推荐做法
import type { FormInstance } from 'element-plus'
const formRef = ref<FormInstance>()

// 安全调用
formRef.value?.validate()
```

**总结**：`FormInstance` 是 Element Plus 为开发者提供的**稳定、安全的类型接口**，专门用于表单操作，避免了直接操作组件内部实现可能带来的副作用（包括你遇到的样式问题）。

# 五、script中使用组件实例

当在组件中使用组件的实例的时候，默认是不会有样式的，因为就没有引入过组件的样式，这个时候就需要导入样式，导入样式有下面几种方法

## 5.1 全局样式引入

方案一：在 main.ts 中全局引入（推荐用于简单项目）

```ts
// main.ts
import { createApp } from 'vue'
import App from './App.vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'  // 引入全部样式

const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

方案二：在 CSS 文件中全局引入

```css
/* style.css 或 main.css */
@import 'element-plus/dist/index.css';
```

## 5.2 按需样式引用

### 在组件中手动引入

例如 ElMessage 的实例样式引用(<mark class="hltr-cyan">一般是在反馈组件</mark>)：

```vue
<script setup lang="ts">
import { ElMessage, type FormInstance, type FormRules } from "element-plus";
// 手动引入 ElMessage 样式
import 'element-plus/es/components/message/style/css'

const formRef = ref<FormInstance>()

function showMessage() {
  ElMessage.success('操作成功')
}
</script>
```

### 使用插件自动导入(推荐)

下载 unplugin-element-plus 插件：

```bash
npm instrall unplugin-element-plus
```

在 vite 里面进行配置：

```ts
// vite.config.ts
import ElementPlus from 'unplugin-element-plus/vite'

export default {
  plugins: [
    ElementPlus({
      // options
    }),
  ],
}
```

其他选项：https://github.com/element-plus/unplugin-element-plus/blob/main/README.zh-CN.md


# 六、特殊样式

在 Element-Plus 中，有一些样式是设置到 `id='app'` 之外，就是不在组件渲染的结构中，这种渲染在 [[02 Vue内置组件Teleport|Vue内置组件Teleport]] 中有这种的渲染方法。

这个时候如果使用常用的 css 选择器，是不能选择到需要的 class ，这个时候就需要使用到 `:global` 来全局选择

|               |                                                          |
| ------------- | -------------------------------------------------------- |
| **`:global`** | **CSS Modules 的语法**，用于在模块化 CSS 中声明一个选择器是**全局的**，不会被哈希转换。 |

比如在 Vue 的项目中，在父子组件，或者在 app 结构之外的组件，要选择一个唯一 class 或者 id ，就可以使用这个语法：

```CSS
//因为el-dropdown-menu_item在app结构之外
//要到全局寻找，所以需要用:global来修改
:global(.el-dropdown-menu__item) {
  line-height: 36px !important;
  padding: 6px 22px;
}
```


