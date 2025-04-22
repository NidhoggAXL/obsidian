# 一、认识 HTTPS
HTTP 协议是明文传输的，不安全，有时候我们需要安全的传输数据

**怎么样才叫安全的传输数据?**

* 收发双方需要互相鉴别，防止冒充者
* 确保收发双方的报文在传输期间没有被篡改
* 确保收发双方的敏感信息不被冒充者窃听

使用 HTTPS 协议可以实现数据的安全传输

**超文本传输安全协议 Hyper Text Transfer Protocol Secure**

**HTTPS = HTTP + SSL/TLS**

**HTTPS 在 HTTP 的基础上使用 SSL/TLS 来加密和解密报文**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716382008000mcyr3c.png)


**HTTPS = HTTP + SSL/TLS，默认端口号是 443**

SSL:安全套接字层协议 Secure Sockets Layer

TLS:传输层安全协议 Transport Layer Security

在 SSL 基础上设计了 TLS 协议

SSL/TLS 也可以和其他协议配合使用，比如FTPS、SMTPS

**HTTPS 是如何保证安全的呢？**

* HTTPS 在 HTTP 的基础上使用 SSL/TLS 来加密和解密报文
* 常见的加密方式有对称加密和非对称加密

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716382184000b15c2n.png)


# 二、对称加密和非对称加密
**对称加密：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716382260000kfmazu.png)


对称加密使用同一个秘钥来加密和解密

对称加密算法有:RC4、DES、3DES、AES 等加密算法

根据同一个秘钥将明文加密成密文，或将密文解密成明文

发送端加密，接收端解密，这个秘钥由发送端生成

接收端为了解密，必须拿到发送端生成的这个秘钥

**对称秘钥如何传输?明文传输?密文传输?**

* 对称秘钥如果明文传输，可以被第三方拿到，使得第三方也可以解密密文
* 对称秘钥如果密文传输，问题又回来了，接收端如何解密秘钥?
* 我们无法直接使用对称加密来保证安全传输

**非对称加密**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716382444000uinq9b.png)

非对称加密使用公钥和私钥两种秘钥，它们并不是同一个秘钥

公钥用来加密明文，私钥用来解密密文

公钥一般是公开的，都能拿到，私钥只有接收端才有，不公开

**公钥和私钥是一对，是一一对应的**

使用公钥加密，必须使用**对应的私钥**才能解密

使用私钥加密的密文，也必须**使用对应的公钥**才能解密

非对称加密算法有:RSA、DH 等

非对称加密的加解密速度比对称加密要慢

**非对称加密的原理：**

* 发送端使用公钥加密，接收端使用私钥解密
* 公钥和私钥由接收端生成，公钥明文传输给发送端
* 发送端使用公钥加密后发送到接收端，接收端使用私钥解密
* 公钥被第三方截获也没关系，因为第三方没有私钥

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716382810000a6161j.png)


**混合加密：**

* 非对称加密可以安全的传输秘钥，但是加解密速度慢
* 对称加密不能安全的传输秘钥，但是加解密速度快
* 使用非对称加密解决对称秘钥的传输问题，使用对称加密传输数据
* SSL/TLS 使用的就是混合加密

 ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716383049000v4g427.png)

# 三、数字签名
使用混合加密，我们可以防止传输的消息被窃听。如何确定传输的消息没有被篡改过，又如何确认是对方发送的呢?需要使用**数字签名**

* 发送端计算消息的散列值，使用发送端生成的私钥加密，得到消息的签名
* 发送端将签名和对称秘钥加密后的消息传输到接收端
* 接收端将接收到的消息用同样的方式计算出散列值
* 接收端使用发送端公钥解密签名，得到另一个值，比较这两个值是否一致

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716383957000chre8m.png)

* 比对一致则表明消息是对方发过来的，也没有被篡改过
* 接收端使用发送端公钥能解密签名值，表明收到的就是发送端的消息
* 散列值一致则保证了消息没有被篡改过


# 四、证书
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716384391000i3hky2.png)

如何保证公钥的合法性?

**就要使用证书：**

* 全称公钥证书，包含姓名、邮箱等个人信息，以及公钥和数字签名
* 证书由认证机构 CA 进行数字签名
* CA 就是能够认定公钥确实属于此人并能够生成数字签名的个人或组织
* 证书需要申请者主动去认证机构注册并下载

**没有第三方时的通信：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716384659000qydiuh.png)

**有第三方时的通信：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716384749000t4pc5h.png)

# 五、Wireshark 中的 HTTPS 
HTTPS 是密文传输的，Wireshark 抓到的都是加密后的包，如果要具体看解密后的包，需要对环境变量进行配置。

