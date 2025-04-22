# 一、ICMP定义
Internet控制消息协议ICMP(Internet Control Message Protocol)是网络层的一个重要协议。ICMP协议用来在网络设备间传递各种差错和控制信息，并对于收集各种网络信息、诊断和排除各种网络故障等方面起着至关重要的作用。使用基于ICMP的应用时，需要对ICMP的工作原理非常熟悉。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715430025000746nj8.png)


# 二、ICMP重定向-控制

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715430168000bcw3jv.png)


ICMP 重定向是一种 ICMP 消息，用于告知主机其应该通过不同的路由器到达特定目标。

**工作原理**

当路由器检测到一个主机正在使用不优的路由时，它会发送 ICMP 重定向消息给主机。该消息包含以下信息：

- 目标 IP 地址
- 新的网关 IP 地址
- 重定向类型（主机或网络）

主机收到 ICMP 重定向消息后，它会更新其路由表，将新的网关 IP 地址作为到达目标的默认网关。

> 如上面的例题，当pc端发送数据想给 服务器A 的时候会线向公网的方向，那么就会经过 TRB ，TRB 知道你不是向访问公网，就会使用 ICMP重定向的功能，告诉pc端不要在向这边发送消息，pc端就不会在向 RTB 发送数据。
> * 这样就可以减少路径直接通过路由器 RTA 到达服务器，不用在经过 RTB 在到 RTA 最后到服务器A。
> * 这是次优路径问题

**重定向类型**

有两种类型的 ICMP 重定向：

- **主机重定向：** 重定向一个特定的主机。
- **网络重定向：** 重定向到特定网络的所有主机。

**目的**

ICMP 重定向消息用于：

- 优化路由，减少网络延迟和拥塞。
- 防止路由循环，其中数据包在网络中无限循环。
- 维护网络拓扑信息的准确性。

**优点**

- 提高网络性能。
- 减少路由循环。
- 帮助维护网络拓扑的准确性。

**缺点**

- 主机可能忽略 ICMP 重定向消息，从而导致路由问题。
- 攻击者可能使用欺骗性的 ICMP 重定向消息来劫持流量。

**配置**

ICMP 重定向通常由网络设备（如路由器和防火墙）自动处理。但是，管理员可以配置以下设置：

- 是否允许 ICMP 重定向。
- 是否接受来自特定路由器的 ICMP 重定向。
- 重定向的优先级。

# 三、ICMP差错检测-查询
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715431908000g4q8kh.png)

ping的使用来检测网络是否可达就是这个
```
C:\Users\20764>ping www.baidu.com

Pinging www.a.shifen.com [240e:ff:e020:966:0:ff:b042:f296] with 32 bytes of data:
Reply from 240e:ff:e020:966:0:ff:b042:f296: time=72ms
Reply from 240e:ff:e020:966:0:ff:b042:f296: time=64ms
Reply from 240e:ff:e020:966:0:ff:b042:f296: time=80ms
Reply from 240e:ff:e020:966:0:ff:b042:f296: time=191ms

Ping statistics for 240e:ff:e020:966:0:ff:b042:f296:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
（以毫秒为单位的近似往返时间:）
    Minimum = 64ms, Maximum = 191ms, Average = 101ms
```


| statistics | 统计数字 | minimum | 最小值 |
| ---------- | ---- | ------- | --- |
| packets    | 数据包  | Maximum | 最大值 |
| sent       | 发送   | Average | 平均值 |
| received   | 接收   |         |     |
| lost       | 丢失   |         |     |
|            |      |         |     |

# 四、ICMP错误报告-差错检测

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715432094000qkhyn4.png)


## 4.1 ICMP消息类型和编码类型
![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17154326040001x0jwe.png)

> echo request  回应请求
> echo reply      回应回复

举例：网络不可达

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/171543313900057jais.png)


# 五、ICMP应用-ping
```
C:\Users\20764>ping

Usage: ping [-t] [-a] [-n count] [-l size] [-f] [-i TTL] [-v TOS]
            [-r count] [-s count] [[-j host-list] | [-k host-list]]
            [-w timeout] [-R] [-S srcaddr] [-c compartment] [-p]
            [-4] [-6] target_name

Options:
    -t             Ping the specified host until stopped.
                   To see statistics and continue - type Control-Break;
                   To stop - type Control-C.
    -a             Resolve addresses to hostnames.
    -n count       Number of echo requests to send.
    -l size        Send buffer size.
    -f             Set Don't Fragment flag in packet (IPv4-only).
    -i TTL         Time To Live.
    -v TOS         Type Of Service (IPv4-only. This setting has been deprecated
                   and has no effect on the type of service field in the IP
                   Header).
    -r count       Record route for count hops (IPv4-only).
    -s count       Timestamp for count hops (IPv4-only).
    -j host-list   Loose source route along host-list (IPv4-only).
    -k host-list   Strict source route along host-list (IPv4-only).
    -w timeout     Timeout in milliseconds to wait for each reply.
    -R             Use routing header to test reverse route also (IPv6-only).
                   Per RFC 5095 the use of this routing header has been
                   deprecated. Some systems may drop echo requests if
                   this header is used.
    -S srcaddr     Source address to use.
    -c compartment Routing compartment identifier.
    -p             Ping a Hyper-V Network Virtualization provider address.
    -4             Force using IPv4.
    -6             Force using IPv6.

```

```
ping -c 代表ping几个
ping -a TTL的指定值，默认255
ping -f 不分片
ping -r 记录路由
ping -s 定义数据包的一个大小，默认56个字节
```

**Ping** 是一个网络诊断工具，使用 ICMP（Internet 控制消息协议）来测试主机之间的连接性和响应时间。

**工作原理**

Ping 向目标主机发送 ICMP 回显请求消息。目标主机收到请求后，将发送一个 ICMP 回显响应消息给源主机。

Ping 测量从发送回显请求到收到回显响应所需的时间，称为往返时间 (RTT)。

**用途**

Ping 用于：

- 测试主机之间的连接性。
- 测量网络延迟和数据包丢失。
- 诊断网络问题。

**优点**

- 易于使用。
- 不需要在目标主机上运行任何特殊软件。
- 可以快速提供有关网络连接和响应时间的信息。

**缺点**

- 无法确定数据包丢失的确切原因。
- 某些网络设备可能会阻止或修改 ICMP 消息，从而影响 Ping 的准确性。

**使用**

在命令提示符下输入以下命令来使用 Ping：

```
ping <目标主机或 IP 地址>
```

例如，要测试到 [www.example.com](http://www.example.com/) 的连接性，请输入以下命令：

```
ping www.example.com
```

Ping 将发送一系列 ICMP 回显请求消息并显示以下信息：

- 目标主机的 IP 地址。
- 往返时间 (RTT)。
- 数据包丢失率。

**示例输出**

以下是一个使用 Ping 测试到 [www.example.com](http://www.example.com/) 连接性的示例输出：

```
Pinging www.example.com [93.184.216.34] with 32 bytes of data:
Reply from 93.184.216.34: bytes=32 time=20ms TTL=56
Reply from 93.184.216.34: bytes=32 time=22ms TTL=56
Reply from 93.184.216.34: bytes=32 time=21ms TTL=56
Reply from 93.184.216.34: bytes=32 time=23ms TTL=56

Ping statistics for 93.184.216.34:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 20ms, Maximum = 23ms, Average = 21ms
```

在这个示例中，Ping 成功连接到 `www.example.com`，并且往返时间 (RTT) 为 20-23 毫秒，数据包丢失率为 0%。

# 六、ICMP应用-Tracert
是一个路由跟踪，知道主机A访问主机B路径是怎么走的

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17154336550009i7vrj.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715433692000axt798.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1715433747000lro4o8.png)

> Tracert显示数据包在网络传输过程中所经过的每一跳（默认跟踪30跳）


**Tracert**（跟踪路由）是一个网络诊断工具，使用 ICMP（Internet 控制消息协议）来确定数据包从源主机到目标主机的路径。

**工作原理**

Tracert 向目标主机发送一系列 ICMP 回显请求消息，每个消息都有一个不同的生存时间 (TTL) 值。TTL 值指定数据包可以在网络中经过的最大路由器跳数。

当数据包到达路由器时，路由器会将 TTL 值减一。如果 TTL 值变为零，路由器将丢弃数据包并发送一个 ICMP 超时消息给源主机。

Tracert 监听 ICMP 回显响应和 ICMP 超时消息。通过分析这些响应，Tracert 可以确定数据包经过的路由器路径。

**用途**

Tracert 用于：

- 诊断网络连接问题。
- 识别网络延迟和数据包丢失的原因。
- 跟踪数据包在网络中的路径。
- 识别网络中的路由循环。

**优点**

- 易于使用。
- 不需要在目标主机上运行任何特殊软件。
- 可以提供有关网络路径和延迟的有价值信息。

**缺点**

- 可能无法确定数据包丢失的确切原因。
- 某些网络设备可能会阻止或修改 ICMP 消息，从而影响 Tracert 的准确性。

**使用**

在命令提示符下输入以下命令来使用 Tracert：

```
tracert <目标主机或 IP 地址>
```

例如，要跟踪到 `www.example.com`的路径，请输入以下命令：

```
tracert www.example.com
```

Tracert 将显示数据包经过的路由器路径、每个跳的 IP 地址和传输延时。

**示例输出**

以下是一个使用 Tracert 跟踪到 `www.example.com` 路径的示例输出：

```
Tracing route to www.example.com [93.184.216.34]
over a maximum of 30 hops:

  1    <1 ms    <1 ms    <1 ms  192.168.1.1
  2     1 ms     1 ms     1 ms  10.0.0.1
  3     2 ms     2 ms     2 ms  203.0.113.1
  4     3 ms     3 ms     3 ms  203.0.113.2
  5    10 ms    10 ms    10 ms  203.0.113.3
  6    11 ms    11 ms    11 ms  203.0.113.4
  7    12 ms    12 ms    12 ms  203.0.113.5
  8    13 ms    13 ms    13 ms  203.0.113.6
  9    14 ms    14 ms    14 ms  203.0.113.7
 10    15 ms    15 ms    15 ms  203.0.113.8
 11    16 ms    16 ms    16 ms  203.0.113.9
 12    17 ms    17 ms    17 ms  203.0.113.10
 13    18 ms    18 ms    18 ms  203.0.113.11
 14    19 ms    19 ms    19 ms  203.0.113.12
 15    20 ms    20 ms    20 ms  203.0.113.13
 16    21 ms    21 ms    21 ms  203.0.113.14
 17    22 ms    22 ms    22 ms  203.0.113.15
 18    23 ms    23 ms    23 ms  203.0.113.16
 19    24 ms    24 ms    24 ms  203.0.113.17
 20    25 ms    25 ms    25 ms  203.0.113.18
 21    26 ms    26 ms    26 ms  203.0.113.19
 22    27 ms    27 ms    27 ms  203.0.113.20
 23    28 ms    28 ms    28 ms  203.0.113.21
 24    29 ms    29 ms    29 ms  203.0.113.22
 25    30 ms    30 ms    30 ms  203.0.113.23
 26    31 ms    31 ms    31 ms  203.0.113.24
 27    32 ms    32 ms    32 ms  203.0.113.25
 28    33 ms    33 ms    33 ms  203.0.113.26
 29    34 ms    34 ms    34 ms  93.184.216.34 [www.example.com]

Trace complete.
```

在这个示例中，Tracert 成功跟踪到 `www.example.com` 的路径，并显示了目标主机的 IP 地址和主机名。

# 七、Win10和VRP系统的tracert的不同
WIN10是用ICMP请求报文，TTL逐渐增加的方式进行跟踪每跳设备。VRP是使用访问UDP高端口的方式跟踪每一跳设备。

**Windows 10 的 Tracert**

- 使用 ICMP 回显请求消息。
- TTL 值逐渐增加，从 1 开始。
- 当 TTL 值达到路由器时，路由器会将 TTL 值减一并转发数据包。
- 当 TTL 值变为零时，路由器会丢弃数据包并发送一个 ICMP 超时消息给源主机。
- Tracert 监听 ICMP 回显响应和 ICMP 超时消息。
- 通过分析这些响应，Tracert 可以确定数据包经过的路由器路径。

**华为 VRP 系统的 Tracert**

- 使用访问 UDP 高端口的方式。
- 向目标主机发送一个 UDP 数据包，其中端口号从 33434 开始逐渐增加。
- 当 UDP 数据包到达路由器时，路由器会检查端口号。
- 如果端口号是已知的 Tracert 端口（例如 33434），路由器会将数据包转发到下一个路由器。
- 如果端口号不是已知的 Tracert 端口，路由器会丢弃数据包。
- Tracert 监听 UDP 数据包的 ICMP 端口不可达消息。
- 通过分析这些消息，Tracert 可以确定数据包经过的路由器路径。

**主要区别**

Windows 10 的 Tracert 和华为 VRP 系统的 Tracert 之间的主要区别在于它们使用的协议：

- Windows 10 的 Tracert 使用 ICMP，而华为 VRP 系统的 Tracert 使用 UDP。

这两种方法各有优缺点：

- **ICMP Tracert** 更加简单和通用，因为它不需要在目标主机上运行任何特殊软件。但是，它可能无法穿透某些防火墙或网络设备，因为 ICMP 消息可能会被阻止。
- **UDP Tracert** 更加可靠，因为它使用 UDP 端口号来识别数据包。但是，它需要在目标主机上运行一个 Tracert 服务器来接收和响应 UDP 数据包。

在大多数情况下，Windows 10 的 ICMP Tracert 就足够了。但是，如果需要更可靠的跟踪，则可以使用华为 VRP 系统的 UDP Tracert。


# 八、UDP
UDP（用户数据报协议）是一种无连接的传输层协议，用于在网络上发送数据。它与 TCP（传输控制协议）一起工作，为应用程序提供网络通信服务。

**UDP 的特点：**

- **无连接：** UDP 不需要在发送数据之前建立连接。这使得它比 TCP 更快，更轻量级。
- **不可靠：** UDP 不保证数据包的顺序、完整性或可靠性。它只是将数据包发送到网络上，由应用程序负责处理丢失或损坏的数据包。
- **面向报文：** UDP 将数据分割成称为数据报的小块，并独立发送每个数据报。
- **低开销：** UDP 的开销比 TCP 低，因为它不需要维护连接状态或进行错误检查。

**UDP 的优点：**

- **速度快：** UDP 不需要建立连接，因此比 TCP 更快。
- **轻量级：** UDP 的开销比 TCP 低，因为它不需要维护连接状态或进行错误检查。
- **适用于实时应用：** UDP 适用于需要快速响应时间的实时应用程序，例如在线游戏和视频流。

**UDP 的缺点：**

- **不可靠：** UDP 不保证数据包的顺序、完整性或可靠性。
- **不适合传输大数据：** UDP 不适合传输大数据，因为数据包可能会丢失或损坏。

**UDP 的应用：**

UDP 用于各种应用程序，包括：

- **在线游戏：** UDP 用于在线游戏中，因为它可以提供快速、低延迟的通信。
- **视频流：** UDP 用于视频流，因为它可以处理数据包丢失，同时仍然提供流畅的视频体验。
- **语音通话：** UDP 用于语音通话，因为它可以提供低延迟的通信。
- **DNS 查询：** UDP 用于 DNS 查询，因为它是一种快速、轻量级的协议。

UDP 是一种重要的协议，用于各种需要快速、低延迟通信的应用程序。


# 九、例题
ICMP 可以检测MTU，支持重定向，ICMP的消息可以分为两类，一是用于诊断是否有错的查询消息，即查询报文;二是通知出错原因的消息，即差错报文。

