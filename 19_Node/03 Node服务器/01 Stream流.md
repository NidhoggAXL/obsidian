# 一、认识Stream

什么是Stream（小溪、小河，在编程中通常翻译为流）呢？

 - 我们的第一反应应该是**流水，源源不断的流动**；
 - 程序中的流也是类似的含义，可以想象当我们从一个文件中读取数据时，文件的二进制（字节）数据会源源不断的被读取到我们程序中；
 - 而这个一连串的字节，就是我们程序中的流；

> [!tip] 可以这样理解流：
 > - 是**连续字节的一种表现形式和抽象概念**；
 > - 流应该是**可读的**，也是**可写的**；

在之前学习文件的读写时，我们可以直接通过 readFile 或者 writeFile 方式读写文件，为什么还需要流呢？

 - 直接读写文件的方式，虽然简单，但是无法控制一些细节的操作；
 - 比如从什么位置开始读、读到什么位置、一次性读取多少个字节；
 - 读到某个位置后，暂停读取，某个时刻恢复继续读取等等；
 - 或者这个文件非常大，比如一个视频文件，一次性全部读取并不合适；

# 二、读写的Stream

事实上Node中很多对象是基于流实现的：http模块的Request和Response对象；

官方文档：<mark class="hltr-cyan">另外所有的流都是EventEmitter的实例</mark>，可以使用和EventEmitter的所有方法。

Node.js中有四种基本流类型：

 - **Writable**：可以向其写入数据的流（例如 fs.createWriteStream()）。
 - **Readable**：可以从中读取数据的流（例如 fs.createReadStream()）。
 - **Duplex**：同时为Readable和Writable（例如 net.Socket）。
 - **Transform**：Duplex可以在写入和读取数据时修改或转换数据的流（例如zlib.createDeflate()）。

# 三、Readable

之前我们读取一个文件的信息：

```js
fs.readFile("./text.txt", { encoding: "utf-8" }, (err, data) => {
  if (err) return;
  console.log(data);
});
```

这种方式是一次性将一个文件中所有的内容都读取到程序（内存）中，但是这种读取方式就会出现我们之前提到的很多问题：**文件过大、读取的位置、结束的位置、一次读取的大小**；

这个时候，我们可以使用 createReadStream，我们来看几个参数，更多参数可以参考官网：

 - **start**：文件读取开始的位置(字节)；
 - **end**：文件读取结束的位置(字节)；
 - **highWaterMark**：一次性读取字节的长度(字节)，默认是64kb(64字节)；
 - **encoding**：读取到数据解码方式。

创建文件的Readable:

```js
import fs from 'fs'

const readStream = fs.createReadStream("./aaa.txt", {
  start: 2,
  end: 9,
  encoding: "utf-8",
  highWaterMark: 3
})

```

## data监听

获取数据：监听 data 事件，获取到读取到的数据

```js
// 监听获取到数据
readStream.on("data", (chunk) => {
  console.log(chunk)
  //llo
  //,le
  //im
})
```

## open、end、close监听

也可以做一些其他的操作：监听其他事件、暂停或者恢复

```js
readStream.on("open", (fd) => {
  console.log("文件打开", fd)//fd文件描述符
  //文件打开 3
})

readStream.on("data", (chunk) => {
  console.log(chunk)
  //llo
  //,le
  //im
})

readStream.on("end", () => {
  console.log("读取完成")
  //读取完成
})

readStream.on("close", () => {
  console.log("文件关闭")
  //文件关闭
})
```

---

## pause、resume方法

```js
readStream.on("data", (chunk) => {
  console.log(chunk)
  readStream.pause()//读取暂停
  setTimeout(() => {
    readStream.resume()//读取恢复
  }, 2000);
})
```

# 四、Writable

之前我们写入一个文件的方式是这样的：

```js
import fs from 'fs'

fs.writeFile("./bbb.txt", "内容", (err) => {
  if (err) {
    console.log("写入失败=>", err)
  }
})
```

这种方式相当于一次性将所有的内容写入到文件中，但是这种方式也有很多问题：比如我们希望一点点写入内容，精确每次写入的位置等；

这个时候，我们可以使用 createWriteStream，我们来看几个参数，更多参数可以参考官网：

 - flags：默认是 w，如果我们希望是追加写入，可以使用 a 或者 a+；
 - start：写入的位置；

案例：一个简单的写入：

```js
const writerStream = fs.createWriteStream("./ccc.txt", {
  flags: "w",
  encoding: "utf-8",
})
writerStream.write("雷姆", err => {
  if (err) {
    console.log("写入失败=>", err);
  }
})

```

## open监听

监听 open 事件

```js
writerStream.on("open", () => {
  console.log("文件打开成功")
})
```

## close、finish监听

我们会发现，我们并不能监听到 close 事件：

 - 这是因为**写入流在打开后是不会自动关闭的**；
 - 我们**必须手动关闭**，来告诉Node已经写入结束了；
 - 并且会发出一个 **finish 事件**的；

```js
writerStream.on("finish", () => {
  console.log("文件写入结束")
})
writerStream.on("close", () => {
  console.log("文件关闭")
})

writerStream.close()
```

## end方法

另外一个非常常用的方法是 end：end方法相当于做了两步操作： **write传入的数据和调用close方法；**

```js
writerStream.on("open", () => {
  console.log("文件打开成功")
})

writerStream.end("雷姆")

writerStream.on("finish", () => {
  console.log("文件写入结束")
})
writerStream.on("close", () => {
  console.log("文件关闭")
})
```


# 五、pipe(管)

当我们要进行一个文件的拷贝的时候，有下面的几种方法：

1. 读取到数据后，在写入到文件中

```js
import fs from "fs";

fs.readFile("./ccc.txt", (err, data) => {
  if (err) return;
  fs.writeFile("./ccc-copy.txt", data, (err) => {
    if (err) {
      console.log("写入失败=>", err);
      //写入失败=> null
    }
  });
});
```

2. 可以将读取到的输入流，手动的放到输出流中进行写入：

```js
import fs from "fs";

const readStream = fs.createReadStream("./ccc.txt");
const writeStream = fs.createWriteStream("./ccc-copy01.txt");
readStream.on("data", (data) => {
  writeStream.write(data);
})
```

3. 通过pipe来完成这样的操作（建立管道）：

```js
import fs from "fs";

const readStream = fs.createReadStream("./ccc.txt");
const writeStream = fs.createWriteStream("./ccc-copy02.txt");
// pipe 建立通道
readStream.pipe(writeStream);
```



