![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715436580000nv6wyv.png)


# 一、ARP定义
ARP 地址解析协议（Address Resolution Protocol）是一种网络层协议，用于将 IP 地址解析为 MAC 地址。

在网络中，每个设备都有一个唯一的 MAC 地址，用于在物理层上标识该设备。但是，网络应用程序通常使用 IP 地址来标识设备。ARP 负责将 IP 地址转换为相应的 MAC 地址。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171543678100090rk8t.png)

# 二、ARP数据包格式
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715436827000n9evdq.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17154370690003kkzrm.png)

# 三、ARP工作原理
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715437205000ss0d88.png)


当一台设备需要向另一台设备发送数据时，它会检查其 ARP 缓存，以查看它是否知道目标设备的 MAC 地址。如果它知道，它将使用该 MAC 地址将数据发送到目标设备。

如果一台设备不知道目标设备的 MAC 地址，它会向**网络广播**一个 ARP 请求消息。该消息包含目标设备的 IP 地址。

网络上的所有设备都会收到 ARP 请求消息，但只有目标设备会响应。目标设备会发送一个 ARP 响应消息，其中包含其 MAC 地址。

发送 ARP 请求的设备会将目标设备的 IP 地址和 MAC 地址添加到其 ARP 缓存中，以便下次它需要与该设备通信时可以快速查找 MAC 地址。

## 3.1 ARP缓存表
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715437908000eeg0s6.png)

这就是在路由器里面查看的一个缓存表

expire（到期）单位是分钟。默认是20分钟，可以通过命令修改
# 四、ARP优缺点
**ARP 的优点：**

- **简单易用：** ARP 是一种简单的协议，易于理解和实现。
- **高效：** ARP 缓存可以提高网络性能，因为设备不必每次都广播 ARP 请求。
- **可靠：** ARP 使用广播和响应机制来确保可靠地解析 MAC 地址。

**ARP 的缺点：**

- **广播风暴：** 如果网络上有很多设备，ARP 广播请求可能会导致广播风暴，从而降低网络性能。
- **ARP 欺骗：** 攻击者可以发送虚假的 ARP 响应消息，从而将流量重定向到他们的设备。
# 五、ARP应用
ARP 用于各种网络应用程序，包括：

- **IP 地址到 MAC 地址解析：** 这是 ARP 的主要功能。
- **动态主机配置协议 [[19 HDLC & PPP & PPPOE - 数据链路层|HDLC]]：** DHCP 服务器使用 ARP 来分配 IP 地址和 MAC 地址。
- **网络管理：** 网络管理员可以使用 ARP 来诊断网络问题和管理网络设备。

ARP 是一种重要的协议，用于在网络中解析 IP 地址和 MAC 地址。它使设备能够相互通信，并提高网络性能。

# 六、免费（无故）ARP
免费 ARP 是 ARP（地址解析协议）的一种变体，用于检测网络上是否存在具有特定 IP 地址的设备，而无需实际向该设备发送数据包。

什么时候会发送免费ARP呢？
* 插入网线
* 开机
* 修改ip

**工作原理：**

免费 ARP 请求消息与常规 ARP 请求消息类似，但**目标硬件地址**字段设置为全 0。当一台设备收到免费 ARP 请求时，它会检查其 ARP 缓存，以查看它是否知道具有该 IP 地址的设备。如果它知道，它将发送一个 ARP 响应消息，其中包含其 MAC 地址。

如果网络上没有具有该 IP 地址的设备，则不会有设备响应免费 ARP 请求。

**使用：**

* 免费 ARP 通常由网络管理工具和安全工具使用。它可以用来诊断网络问题、检测 ARP 欺骗攻击和管理网络设备。
* 更新 ARP 缓存：当设备重新配置了一个 IPv4 地址时，它需要更新网络上其他设备的 ARP 缓存。免费 ARP 报文允许设备**广播其新的 IP 地址**和 MAC 地址，以便其他设备可以更新其 ARP 缓存。
* 检测 IP 地址冲突：免费 ARP 报文还可以用来检测 IP 地址冲突。如果网络上已经存在具有相同 IP 地址的设备，则该设备会响应免费 ARP 报文。这将使重新配置其 IP 地址的设备意识到存在 IP 地址冲突，并可以采取措施解决冲突。

# 七、ARP和免费（无故）ARP的区别
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715439571000q81n0a.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1718194927000o5ahnw.png)



