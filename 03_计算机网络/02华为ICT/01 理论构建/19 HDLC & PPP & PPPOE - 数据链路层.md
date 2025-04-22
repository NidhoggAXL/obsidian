
广域网中经常会使用串行链路来提供远距离的数据传输，高级数据链路控制HDLC(High-Level Data Link Control)和点对点协议PPP(Point to PointProtocol)是两种典型的串口封装协议。
# 一、HDLC 链路
串行链路的数据传输方式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168762660002z0ggo.png)

HDLC协议应用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716876402000cq9rfn.png)


HDLC 帧格式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716876486000c5qpjy.png)

HDLC 基本配置

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716876556000gkgrtf.png)

HDLC 接口地址借用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716876587000o2liym.png)


配置验证·

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716876615000i43rof.png)

HDLC 缺点：

* 不支持认证
* 不支持捆绑
* 不支持动态获取地址

# 二、PPP
PPP 应用：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877161000v5ecdr.png)


PPP 组件：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877179000b895c8.png)


PPP 链路建立过程：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877285000rbbduv.png)

* Dead - 死去的、完全的
* Establish - 建立、创建
* Authenticate - 证明是真实的
* Network - 网
* Terminate - 结束、终结
* FALL - 失败
* DOWN - 向下
* CLOSING - closing 关闭



PPP 帧格式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877369000m2fu1e.png)


LCP 报文：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877385000bmi0aq.png)


LCP 协商参数：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877460000m3dgho.png)


LCP链路参数协商：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168776290009guxqk.png)


## 2.1 PPP 认证模式
PPP认证模式-PAP

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716877672000ibkb9m.png)


CHAP 认证

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716878129000xrhbjs.png)

## 2.2 IPCP 地址协商

IPCP 静态地址协商

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716878371000ug0byj.png)


IPCP 动态地址协商：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716878404000g1yqxs.png)

## 2.3 PAP 认证

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716878434000vvaepi.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168784410004pfv78.png)

## 2.4 CHAP 认证

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168784880006hauyn.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716878568000z2o64s.png)

# 三、PPPoE
数字用户线路DSL(Digital Subscriber Line)是以电话线为传输介质的传输技术，人们通常把所有的DSL技术统称为xDSL，x代表不同种类的数字用户线路技术。目前比较流行的宽带接入方式为ADSL，ADSL是非对称DSL技术，使用的是PPPoE(PPPoverEthernet)协议。

PPPOE协议通过在以太网上提供点到点的连接，建立PPP会话，使得以太网中的主机能够连接到远端的宽带接入服务器上。PPPOE具有适用范围广安全性高、计费方便等特点。


PPPoE 应用场景

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168789940005etf1h.png)

PPPoE在DSL中的应用

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716879070000boylcn.png)


PPPoE报文

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168792040002xt8bv.png)

PPPOE会话建立过程

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168792870005rj08i.png)

| 英语       | 翻译  |
| -------- | --- |
| discover | 发现  |
| session  | 会话  |
|          |     |


PPPoE协议报文

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716879969000wle12m.png)

PPPoE发现阶段

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168799760004538ko.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168800170009gx0dc.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716880036000jcqbd6.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716880046000xmqkbb.png)


PPPOE会话终结

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716880122000npu7xx.png)

PPPoE会话建立过程

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716880140000ot4kw4.png)

PPPoE 配置

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171688032400012fku2.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168803920006uqpav.png)

