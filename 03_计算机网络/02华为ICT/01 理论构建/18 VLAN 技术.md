
# 一、VLAN 原理和配置

随着网络中计算机的数量越来越多，传统的以太网络开始面临冲突严重广播泛滥以及安全性无法保障等各种问题。

VLAN(Virtual LocalArea Network)即虚拟局域网，是将一个物理的局域网在逻辑上划分成多个广播域的技术。通过在交换机上配置VLAN，可以实现在同一个VLAN内的用户可以进行二层互访，而不同VLAN间的用户被二层隔离。这样既能够隔离广播域，又能够提升网络的安全性。


传统以太网

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716795726000zckldh.png)


VLAN 技术

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716795741000rsvtsf.png)


VALN 帧格式

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716796065000inqugn.png)

> tag 标签在从发送端发给接收端的时候是打上tag的，后面在发出时移除标签



链路类型：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17167963790001v9fqj.png)


端口类型-Access

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716817937000tjxb4j.png)

端口类型-Trunk

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716818043000j0xjiv.png)


端口类型-Hybrid

* 看成 access 和 trunk 的结合体

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716819067000x101rj.png)

**hybrid接口接收帧时:**

* 收到一个Untagged帧,加上PVID的Tag,然后查看是否在Untagged或Tagged 列表中,如果在则转发,如果不 在直接丢弃
* 收到一个Tagged帧，检查是否在Untagged或Tagged 列表中,如果在则转发,如果不在直接丢弃

**发送帧时:**

* 如果这个帧的VID不在Untagged或Tagged 列表中，则直接丢弃
* 如果这个帧的VID在Untagged 列表中，剥离Tag后发送出去。
* 如果这个帧的VID在Tagged列表中，带Tag直接发送出去。

**voice VLAN 应用：**

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17168724330002tnrv4.png)

配置 voice vlan 

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716872495000g9xrgm.png)


配置验证

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716872555000r6wghe.png)


# 二、VLAN 单臂路由

部署了VLAN的传统交换机不能实现不同VLAN间的二层报文转发，因此必须引入路由技术来实现不同VLAN间的通信。VLAN路由可以通过二层交换机配合路由器来实现，也可以通过三层交换机来实现。


VLAN 局限性：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171687287900052ss3l.png)

VLAN路由-每个VLAN一个物理连接

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716872935000otco9g.png)

VLAN 单臂路由

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716873897000yzutmm.png)


VLAN 三层交换

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1716874569000ju0gb7.png)


配置三层交换

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171687560800078a0m5.png)


