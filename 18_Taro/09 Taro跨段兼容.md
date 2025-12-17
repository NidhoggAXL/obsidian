# 一、跨端兼容方案

Taro 的设计初衷就是为了**统一跨平台**的开发方式，并且已经尽力通过运行时框架、组件、API 去抹平多端差异，但是由于不同的平台之间还是存在一些无法消除的差异，所以为了更好的实现跨平台开发，Taro 中提供了如下的解决方案。

**方案一：内置环境变量**

 - Taro 在编译时提供了一些**内置的环境变量**来帮助用户做一些特殊处理。
 - 通过这个变量来区分不同环境，从而使用不同的逻辑。**在编译阶段，会移除不属于当前端的代码，只保留当前端的代码**。
 - 内置环境变量虽然可以解决大部分跨端的问题，但是会让代码中存在很多逻辑判断的代码，影了响代码的可维护性，而且也**让代码变得丑陋**。
 - 为了解决这种问题，Taro 提供了另外一种跨端开发的方式作为补充。

**方案二：统一接口的多端文件**

 - 开发者可以通过将文件修改成 **原文件名 + 端类型** 的命名形式（端类型对应着 process.env.TARO_ENV 的取值），不同端的文件代码对外保持统一接口，而引用的时候仍然是 import 原文件名的文件。
 - Taro 在编译时，会跟根据当前编译平台类型，**精准加载对应端类型的文件**，从而达到不同的端加载其对应端的文件。

# 二、内置环境变量

内置环境变量（ `process.env.TARO_ENV`），该环境变量可直接使用

 - `process.env.TARO_ENV`，用于判断当前的编译平台类型，有效值为：`weapp / swan / alipay / tt / qq / jd / h5 / rn`。
 - 通过这个变量来区分不同环境，从而使用不同的逻辑。
 - 在编译阶段，会移除不属于当前平台的代码，只保留当前平台的代码。

```jsx
import { View } from "@tarojs/components";
import { useLoad } from "@tarojs/taro";
import "./index.scss";
import XlButton from "../../components/xl-button";

export default function Index() {
  useLoad(() => {
    console.log("Page loaded.");
  });

  function handleBtnClikc() {
    if (process.env.TARO_ENV === "h5") {
      console.log("显示h5的点击事件")
    } else if (process.env.TARO_ENV === "weapp") {
      console.log("显示weapp的点击事件")
    }
  }

  return (
    <View className="index">
      <XlButton onBtnClick={handleBtnClikc}>我是通用按钮</XlButton>
      {process.env.TARO_ENV === "h5" && (
        <>
          <XlButton type="primary">我是h5显示的按钮</XlButton>
        </>
      )}
      {process.env.TARO_ENV === "weapp" && (
        <>
          <XlButton type="skyblue">我是weapp显示的按钮</XlButton>
        </>
      )}
    </View>
  );
}

```

> [!tip] 注意事项：**不要解构 process.env 来获取环境变量**，请直接以完整书写的方式（process.env.TARO_ENV）来进行使用。


# 三、统一接口的多端文件

统一接口的多端文件这一跨平台兼容写法有如下三个使用要点：

 - 不同端的对应文件**一定要统一接口和调用方式**。
 - 引用文件的时候，只需写默认文件名，不用带文件后缀。
 - **最好有一个平台无关的默认文件**，这样在使用 TS 的时候也不会出现报 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765950192000gkguev.png)

## 3.1 多端组件

- 多端组件（属性，方法，事件等需统）： 针对不同的端写不同的组件代码

```jsx title = "index.jsx"
import { Button } from "@tarojs/components";
import { memo } from "react";

const XlView = memo(() => {
  function handleButtonBtn() {
    console.log("XlView按钮点击");
  }
  return <Button onClick={handleButtonBtn}>XlView</Button>;
});

export default XlView;

```

```jsx title="index.h5.jsx"
import { Button } from '@tarojs/components'
import { memo } from 'react'

const XlView = memo(() => {
  function handleButtonBtn() {
    console.log("h5 XlView按钮点击")
  }
  return (
    <Button onClick={handleButtonBtn}>XlView - h5</Button>
  )
})

export default XlView

```

```jsx title = "index.weapp.jsx"
import { Button } from "@tarojs/components";
import { memo } from "react";

const XlView = memo(() => {
  function handleButtonBtn() {
    console.log("weapp XlView按钮点击");
  }
  return <Button onClick={handleButtonBtn}>XlView - weapp</Button>;
});

export default XlView;

```

使用的时候，正常使用就可以：

```jsx
<XlView></XlView>
```

## 3.2 多端脚本

多端脚本逻辑（属性、方法等需统一） ：针对不同的端写不同的脚本逻辑代码

> [!tip] 和 多端组件 使用情况相同。




