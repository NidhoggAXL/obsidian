# 一、数据二进制

计算机中所有的内容：文字、数字、图片、音频、视频最终都会使用二进制来表示。

JavaScript可以直接去处理非常直观的数据：比如字符串，我们通常展示给用户的也是这些内容。

不对啊，JavaScript不是也可以处理图片吗？

 - 事实上在网页端，图片我们一直是交给浏览器来处理的；
 - JavaScript或者HTML，只是负责告诉浏览器一个图片的地址；
 - **浏览器负责获取这个图片，并且最终讲这个图片渲染出来**；

但是对于服务器来说是不一样的：

 - **服务器要处理的本地文件类型相对较多;**
 - 比如某一个保存文本的文件并不是使用 utf-8 进行编码的，而是用 GBK，那么我们必须读取到他们的二进制数据，再通过GKB转换成对应的文字；
 - 比如我们需要读取的是一张图片数据（二进制），再通过某些手段对图片数据进行二次的处理（裁剪、格式转换、旋转、添加滤镜），**Node中有一个Sharp的库，就是读取图片或者传入图片的 Buffer 对其再进行处理**；
 - 比如在Node中通过TCP建立长连接，TCP传输的是字节流，我们需要将数据转成字节再进行传入，并且需要知道传输字节的大小（客服端需要根据大小来判断读取多少内容）；


# 二、Buffer和二进制

对于前端开发来说，**通常很少会和二进制直接打交道**，但是对于服务器端为了做很多的功能，**我们必须直接去操作其二进制的数据**；

所以Node为了可以方便开发者完成更多功能，提供给了我们一个类Buffer，并且它是全局的。

我们前面说过，Buffer中存储的是二进制数据，那么到底是如何存储呢？

 - 我们可以将Buffer看成是一个存储二进制的数组；
 - 这个数组中的每一项，可以保存8位二进制：`0000 0000`

为什么是8位呢？

 - 在计算机中，很少的情况我们会直接操作一位二进制，因为一位二进制存储的数据是非常有限的；
 - 所以通常会将8位合在一起作为一个单元，这个单元称之为一个字节（byte）；
 - 也就是说 1byte = 8bit，1kb=1024byte，1M=1024kb；
 - 比如很多编程语言中的int类型是4个字节，long类型时8个字节；
 - 比如TCP传输的是字节流，在写入和读取时都需要说明字节的个数；
 - 比如RGB的值分别都是255，所以本质上在计算机中都是用一个字节存储的；

# 三、Buffer和字符串


Buffer相当于是一个字节的数组，数组中的每一项对应一个字节的大小：

如果我们希望将一个字符串放入到Buffer中，是怎么样的过程呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176605632200018bcdq.png)

> [!tip] 会报下面的警告， new Buffer 已经不推荐使用
>  Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766056415000ridpu2.png)

## 3.1 中文呢？

> [!abstract]
> 三个字符对应一个中文，如果是偏门的字就需要多个字符对应一个中文

默认编码：utf-8

```js
const buffer = Buffer.from("敖选龙")
console.log(buffer)//<Buffer e6 95 96 e9 80 89 e9 be 99>
console.log(buffer.toString())//敖选龙
```

如果编码和解码不同：会解析出错误的字符

```js
const buffer = Buffer.from("敖选龙", "utf-16le")
console.log(buffer)//<Buffer 56 65 09 90 99 9f>
console.log(buffer.toString("utf-8"))//Ve      ���
```


# 四、Buffer的其他创建

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17660568450002rnrz3.png)

# 五、Buffer.alloc

Buffer.alloc: 创建了一个8位长度的Buffer，里面所有的数据默认为00；

```js
const buf = Buffer.alloc(8)
console.log(buf)
//<Buffer 00 00 00 00 00 00 00 00>
```

也可以对其进行操作:

```js
const buf = Buffer.alloc(8)
buf[0] = 'w'.charCodeAt()
buf[1] = 100
buf[2] = 0x66
console.log(buf)
//<Buffer 77 64 66 00 00 00 00 00>

console.log(buf[1])//100
console.log(buf[0].toString())//119
console.log(buf[2].toString(16))//66
```

# 六、Buffer和文件读取

文本文件的读取：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766057718000mxqbk2.png)

图片文件的读取

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766057726000to8csb.png)

# 七、Buffer源码

## 7.1 Buffer的创建过程

事实上我们创建Buffer时，并不会频繁的向操作系统申请内存，它会默认先申请一个 `8 * 1024` 个字节大小的内存，也就是8kb

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176605911000049lu3h.png)

## 7.2 Buffer.from源码

假如我们调用Buffer.from申请Buffer：

 - 这里我们以从字符串创建为例
 - node/lib/buffer.js：290行

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176605915400023fya4.png)

## 7.3 fromString的源码

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17660591700008uqv2z.png)


## 7.4 fromStringFast

接着我们查看fromStringFast：

 - 这里做的事情是判断剩余的长度是否还足够填充这个字符串；
 - 如果不足够，那么就要通过 createPool 创建新的空间；
 - 如果够就直接使用，但是之后要进行 poolOffset的偏移变化；
 - node/lib/buffer.js：428行

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766059198000d0z275.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1766059205000yr5wue.png)


