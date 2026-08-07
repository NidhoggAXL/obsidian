# 一、组件及生命周期

在 Taro中，除了应用和页面组件有生命周期之外， **Taro 的组件也是生命周期**，如下图所示：

下面我们来编写一个HYButton组件。

 - 创建组件
 - 定义属性
 - 样式编写
 - 定义插槽
 - 定义生命周期
 - 组件可编写页面生命周期吗？
	 - class组件默认不行，需要单独处理
	 - 但是函数组件是支持的
 - 页面可以编写组件生命周期吗？可以

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765890807000cvfzu3.png)

为了后面方便使用需要先安装两个库：[[07 classnames库使用|classnames]]、protypes

```bash
yarn install classnames

yarn install proptypes
```


使用 CSS Module 编写组件的样式：

```css
.btn {
  color: red;
  font-size: 20px;
  background-color: yellow;
  border: 1px solid black;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;

  .text {
    font-size: 40px;
    font-weight: 700;
  }
}

.primary {
  background-color: blue;
}

.default {
  background-color: green;
}

```

组件的定义：

```jsx
import { Button, Text } from "@tarojs/components";
import classNames from "classnames";
import { memo, useEffect } from "react";
import styles from "./index.module.scss";
import { useDidHide, useDidShow, useLoad, useUnload } from "@tarojs/taro";

const XlButton = memo((props) => {
  // 外部传递出来数据
  const { type = "default", onBtnClick } = props;
  //监听按钮点击，并向外部传递数据

  const handleButtonBtn = () => {
    // 外部点击事件，可以传递数据
    onBtnClick();
  };

  //生命周期
  // React组件的生命周期
  useEffect(() => {
    console.log("useEffect 按钮组件加载完成");
    return () => {
      console.log("useEffect 按钮组件卸载完成");
    };
  });
  // 小程序的页面周期
  useLoad(() => {
    console.log("useLoad 页面加载完成");
  });
  useDidShow(() => {
    console.log("useDidShow 页面加载完成");
  });
  useDidHide(() => {
    console.log("useDidHide 页面加载完成");
  });
  useUnload(() => {
    console.log("useUnload 页面加载完成");
  });

  return (
    <Button
      className={classNames(styles["btn"], styles[type])}
      onClick={handleButtonBtn}
    >
      {/* 插件的使用 */}
      {props.children || (
        <Text className={classNames(styles["text"])}>按钮</Text>
      )}
    </Button>
  );
});

export default XlButton;
```

使用自定义组件：

```jsx
import { View, Text } from "@tarojs/components";
import { useLoad } from "@tarojs/taro";
import "./index.scss";
import XlButton from "../../components/xl-button";

export default function Index() {
  useLoad(() => {
    console.log("Page loaded.");
  });

  function handleBtnClikc() {
    console.log("外部点击事件");
  }

  return (
    <View className="index">
      <Text>Hello world!</Text>
      <XlButton type="primary" onBtnClick={handleBtnClikc}>
        <Text>我是buton的内容</Text>
      </XlButton>
    </View>
  );
}

```

