# 一、Webpack和Tapable

知道webpack有两个非常重要的类：Compiler和Compilation

 - 他们通过注入插件的方式，来监听webpack的所有生命周期；
 - 插件的注入离不开各种各样的Hook，而他们的Hook是如何得到的呢？
 - 其实是创建了Tapable库中的各种Hook的实例；

所以，如果我们想要学习自定义插件，最好先了解一个库：Tapable

 - Tapable是官方编写和维护的一个库；
 - Tapable是管理着需要的Hook，这些Hook可以被应用到我们的插件中；

# 二、Tapable有哪些Hook呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/177341207700018aonw.png)

# 三、Tapable的Hook分类

同步和异步的：

 - 以 **sync** 开头的，是同步的Hook；
 - 以 **async** 开头的，两个事件处理回调，不会等待上一次处理回调结束后再执行下一次回调；

其他的类别

 - **bail(保释)**：当有返回值时，就不会执行后续的事件触发了；
 - **Loop(循环)**：当返回值为true，就会反复执行该事件，当返回值为undefined或者不返回内容，就退出事件；
 - **Waterfall(瀑布)**：当返回值不为undefined时，会将这次返回的结果作为下次事件的第一个参数；
 - **Parallel**：并行，会同时执行次事件处理回调结束，才执行下一次事件处理回调；
 - **Series**：串行，会等待上一是异步的Hook；

# 四、Hook的使用

需要先安装 tapable 库：

```shell
npm install tapable
```

## 4.1 基本使用

```js
const { SyncHook } = require("tapable")

class Compiler {
  constructor() {
    // 1.创建hook
    this.hooks = {
      // 1.1 创建一个同步的syncHook
      syncHook: new SyncHook(['name', 'age'])
    }

    // 2.注册事件
    this.hooks.syncHook.tap('syncHook', (name, age) => {
      console.log('syncHook', name, age)
    })
    this.hooks.syncHook.tap('syncHook2', (name, age) => {
      console.log('syncHook2', name, age)
    })
  }
}

// 3.触发事件
const compiler = new Compiler()
compiler.hooks.syncHook.call('axl', 18)
```


## 4.2 同步使用

```js
const { SyncLoopHook } = require("tapable");

let count = 0;
class Compiler {
  constructor() {
    // 1.创建hook
    this.hooks = {
      // 1.1 创建一个同步的syncHook
      SyncLoopHook: new SyncLoopHook(["name", "age"]),
    };

    // 2.注册事件
    this.hooks.SyncLoopHook.tap("syncHook", (name, age) => {
      console.log("syncHook1", name, age);
    });
    this.hooks.SyncLoopHook.tap("syncHook2", (name, age) => {
      console.log("syncHook2", name, age);
      if (count < 2) {
        count++;
        return true;
      }
    });
    this.hooks.SyncLoopHook.tap("syncHook3", (name, age) => {
      console.log("syncHook3", name, age);
    });
  }
}

// 3.触发事件
const compiler = new Compiler();
compiler.hooks.SyncLoopHook.call("axl", 18);

```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773474524000nnglc2.png)


## 4.3 异步使用

```js
const { AsyncSeriesHook } = require("tapable");

let count = 0;
class Compiler {
  constructor() {
    // 1.创建hook
    this.hooks = {
      // 1.1 创建一个同步的syncHook
      AsyncSeriesHook: new AsyncSeriesHook(["name", "age"]),
    };

    // 2.注册事件
    this.hooks.AsyncSeriesHook.tapAsync("syncHook", (name, age, callback) => {
      setTimeout(() => {
        console.log("syncHook1", name, age);
        callback();
      }, 1000);
    });
    this.hooks.AsyncSeriesHook.tapAsync("syncHook2", (name, age, callback) => {
      setTimeout(() => {
        console.log("syncHook2", name, age);
        callback()
      }, 2000);
    });
    this.hooks.AsyncSeriesHook.tapAsync("syncHook3", (name, age, callback) => {
      setTimeout(() => {
        console.log("syncHook3", name, age);
        callback()
      }, 3000);
    });
  }
}

// 3.触发事件
const compiler = new Compiler();
compiler.hooks.AsyncSeriesHook.callAsync("axl", 18, () => {
  console.log("全部执行结束");
});
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17734754700008oh17c.png)

