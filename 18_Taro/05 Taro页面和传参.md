# 一、新建page页面

快速创建新页面

1. 命令行创建：Taro create --name [页面名称]
	 - 能够在当前项目的pages目录下快速生成新的页面文件，并填充基础代码，是一个提高开发效率的利器。
2. 手动创建页面
	 - 在目录根目录下的pages目录下新建即可。

注意事项：新建的页面，都需在 app.config.json 中的 pages 列表上配置。

删除页面，需做两件工作

 - 删除页面对应的文件
 - 删除app.config.json中对应的配置

# 二、配置Tabbar

在app.config.js中配置Tabbar

icon路劲支持绝对路径和相对路径

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176588336300041oaht.png)

# 三、页面路由

Taro 有两种页面路由跳转方式：使用Navigator组件跳转、调用API跳转。

 - 组件：Navigator
 - 常用API：navigate 、redirectTo、switchTab、navigateBack

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765883476000987j4m.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1765883480000dsyf56.png)

# 四、页面通讯

## 4.1 url查询字符串

url查询字符串

 - 传递参数：`?name=liujun&id=100`
 - 获取参数：
	 - onLoad 、 useLoad 生命周期获取路由参数
	 - Taro.getCurrentInstance().router.params 获取路由参数。


```js title="正向传递"
// 发送数据
<Navigator url="../home/index?name=axl&age=19">跳转到home页面</Navigator>

import { View, Text } from "@tarojs/components";
import Taro, { useLoad } from "@tarojs/taro";
import "./index.scss";

// 接收数据
export default function Home() {
  useLoad((options) => {
    console.log(options);
  });

  const $instance = Taro.getCurrentInstance();
  console.log($instance.router.params);

  return (
    <View className="home">
      <Text>Hello world!</Text>
    </View>
  );
}

```


```js title = "反向传递"
// 发送数据
export default function Home() {

  function handleBackBtn() {
    // 使用Taro的navigateBack方法实现页面返回
    Taro.navigateTo({
      url: "../index/index", // 指定返回的页面路径
      success: (res) => {
        // 返回成功后的回调函数
        // 通过事件通道向首页发送数据
        res.eventChannel.emit("homeData", {
          data: "home页面的数据", // 要传递的数据内容
        });
      },
    });
  }

  return (
    <View className="home">
      <Text>Hello world!</Text>
      <Button onClick={() => handleBackBtn()}>返回index页面</Button>
    </View>
  );
}

// 接收数据
export default function Index() {
  useLoad(() => {
    console.log("Page loaded.");
    // 监听数据传递
    const eventChannel = Taro.getCurrentInstance().page.getOpenerEventChannel()
    eventChannel.on("homeData", (data) => {
      console.log("home传递过来的数据", data)
    })
  });

  return (
    <View className="index">
      <Text>Hello world!</Text>
      <Navigator url="../home/index?name=axl&age=19" openType="navigate">跳转到home页面</Navigator>
    </View>
  );
}
```


## 4.2 全局事件总线

为了支持**跨组件、跨页面**之间的通信，Taro 提供了**全局事件总线：Taro.eventCenter**

 - Taro.eventCenter.on( eventName, function ) 监听一个事件
 - Taro.eventCenter.trigger( eventName, data) 触发一个事件
 - Taro.eventCenter.off( eventName, function ) 取消监听事件

注意事项：

 - 需先监听，再触发事件，比如：你在A界面触发，然后跳转到B页面后才监听是不行的。
 - 通常on 和 off 是同时使用，可以避免多次重复监听
 - **适合页面返回传递参数、适合跨组件通讯，不适合界面跳转传递参数**
  
```js title="发送数据"
import { View, Text, Button } from "@tarojs/components";
import Taro from "@tarojs/taro";
import "./index.scss";

export default function Home() {

  function handleBackBtn() {
    console.log("hhhhh");
    // 使用Taro的navigateBack方法实现页面返回
    Taro.navigateTo({
      url: "../index/index", // 指定返回的页面路径
      success: () => {
        // 返回成功后的回调函数
        // 通过事件总线通道向首页发送数据
        Taro.eventCenter.trigger("homeData", {
          data: "home页面的数据"
        })
      },
    });
  }

  return (
    <View className="home">
      <Text>Hello world!</Text>
      <Button onClick={() => handleBackBtn()}>返回index页面</Button>
    </View>
  );
}

```

```js title="接收数据"
import { View, Text, Navigator } from "@tarojs/components";
import Taro, { useLoad, useUnload } from "@tarojs/taro";

import "./index.scss";

export default function Index() {
  useLoad(() => {
    console.log("Page loaded.");
    // 监听数据传递
    Taro.eventCenter.on("homeData", getData);
  });

  useUnload(() => {
    // 取消数据监听
    Taro.eventCenter.off("homeData", getData);
  });

  const getData = (data) => {
    console.log("home传递过来的数据", data);
  };

  return (
    <View className="index">
      <Text>Hello world!</Text>
      <Navigator url="../home/index?name=axl&age=19" openType="navigate">
        跳转到home页面
      </Navigator>
    </View>
  );
}

```


