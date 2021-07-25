#  一、绪论



## Internet基本概念

什么是Internet，组成、服务、协议
网络边缘、网络接入（家庭、公司、无线）、网络核心

- 电路交换：预留资源
- 分组交换：存储转发，efficient
- 虚电路：combine

eg. more efficient：slide 51

0.1 active 10Mbps 1Mbps：35个用户中10个用户同时活跃的概率 $$1-\Sigma_{n=0}^{10}  \tbinom{35}{n} 0.1^{n} (1-0.1)^{35-n} \geq 0.04\%$$


## 协议体系结构

- 多层协议体系结构的必要性
- OSI与TCP/IP模型
  -  各层名称、层次之间的关系，以及各层对应功能
  -  两种不同模型的层次之间的对应关系

```
+----------------------------------+
|	Application	layer	应用层	|		（表示层	会话层）
+----------------------------------+
|	Transport layer		传输层	|		
+----------------------------------+
|	Network layer 	 	网络层 |
+----------------------------------+
|	Link layer		  	 链路层 |
+----------------------------------+
|	Physical layer		 物理层 |
+----------------------------------+
```


## 网络性能分析

指标：网络时延、丢包、吞吐量概念
四种时延：处理、排队、传输、传播

传输(Transmission delay)：push all the bits of a packet into a link

​	Packet size / Transmission rate of the link(bps)

传播(Propagation)：one end to another

​	Link length / Propagation speed of link(3*10^8 m/s)

排队：len(queue) = Average rate * Waiting time

处理：微不足道的 Negligible

---

吞吐量：瓶颈线路，一般考察大文件 单传

在任何时间的瞬时吞吐量（instantaneous throughput）是主机接收到一个文件的速率（bps）。如果文件由 F比特组成，主机接收到所有比特用去 $$T$$ 秒，则文件传送的平均吞吐量（average throughput）是 $$F/T$$ bps。

# 二、链路层

链路层服务：分帧（检错码，流控（optional）），媒介访问控制（p2p,广播）[^鸡尾酒]

成帧 ：begin：0111 1110；end：0111 1111.中间如果有连续五个1插0

## 局域网：

局域网的构成：拓扑结构、传输媒介

### 网桥

#### 网桥的作用和工作原理

局域网互联；

工作原理：对收到的帧根据其 MAC 帧的目的地址 进行转发和过滤（网桥根据MAC地址转发，路由器根据网络地址如 IP 地址转发）

#### 路由机制：转发表、地址学习、生成树算法、路由发现机制

地址学习

1. 交换机表初始为空
2. 每个接口接收到的每一个入帧，在交换机表中存储：
   -  该帧源地址字段中的 MAC 地址
   -  该帧到达的接口
   -  当前时间
3. 如果老化期过后，交换机没有接收到以该地址作为源地址的帧，就在表中删除这个地址

生成树算法 Message(Y，d，X)：from X,root Y

### 二三层交换机，基本工作机理

### 比较：Bridge, hub, Layer 2 Switch, Layer 3 Switch, Router

1. Bridge 网桥：连接 LANs（局域网）：转发 地址自学习 ，共享媒介
2. Hub 集线器：Repeater ，物理上是星形的，逻辑上是总线型的 ，每一个传输会占用所有带宽，所有其他站点都会收到；如果两个同时传就会发生碰撞；
3. Layer 2 Switch ：连接主机或 LAN s ：网桥的功能 （链路层的装置、透明、即插即用、自学习） 无碰撞。
4. Layer 3 Switch ：使用到路由器功能的 Switch （交换机 ），填充了 packet forwarding的功能，在 局域网上工作
5. Router ：路由器，在公网或者局域网都能工作

### 令牌环：基本工作原理

## 以太网：

### 媒体接入控制：CSMA的基本思想 

listen before transmit

### CSMA/CD的工作原理

- 冲突检测的方式（2-2-29）

  ◆ 步骤 1 ：如果媒介空闲，传输；否则前往步骤 2
  ◆ 步骤 2 ：如果忙，等待空闲，然后立即传输
  ◆ 步骤 3 ：如果遇到碰撞，发送 jam 信号（6个字节全1的信号），中止
  ◆ 步骤 4 ：发送完 jam 信号以后等待一个随机时间量，然后返回步骤 2

---

- 冲突检测与传播/传输时延的关系

- 二进制指数退避算法： K * 512比特时间 K [0,...,2^n-1] (n<=10)

- 最小帧长和最大范围	

$$
T_{transmission}>2 \times T_{propagation} \;
size \ge 2*L*B/v
$$


### IEEE 802.3以太网规约

802.3 CSMA/CD

- 以太网媒介：connectionless and unreliable既无连接也不可靠

- 以太网帧格式:

  Preamble  |  DstAddress  |  SourceAddress  | type  |  		 Data		  |   CRC

  (7+1)byte  |  		6	 		|		 	6				|	2	|		46~1500	  |	 4

  ![en_US 471](a total review.assets\image-20210618212432523.png)

## 无线局域网

无线局域网的概念和应用
IEEE 802.11体系结构
基本概念
体系结构图
媒体接入控制 CSMA/CA
分布式协调功能
点协调功能
与以太网的 CSMA/CD相比较
802.11b/g频段及传输速率

## 网络传输媒介利用率分析

媒介利用率 $$ U= \frac{T_{transmission}}{total time(T_{transmission}+T_{propagation})} $$

 定义： 1 ：一般化的帧传输时间 a ：端到端的传播时延 N ：站点的个数

Point-to-point link：1/(1+a)

ALOHA, Slotted ALOHA：1/2e；1/e	

令牌环：1/（1+𝑎/𝑁）,𝑎<1；1/（𝑎+𝑎/𝑁）,𝑎>1

CSMA/CD（ p-persistent ）的简单性能模型：1/1+4.44𝑎

# 三、网络层 

交换/路由，转发，建立连接（虚电路） 

网络层向传输层提供主机到主机服务，传输层向应用层提供进程到进程服务

<img src="a%20total%20review.assets/image-20210622170332580.png" style="zoom:35%;" />

## 分组交换网络，基本思想

分组交换网络中路由

- 性能评估指标
- 路由信息的更新方式

## 路由算法

**路由：效率，弹性，稳定**

集中式路由
分布式路由：洪泛，随机行走，自适应路由//动态路由策略与算法
最小代价路由算法及其性能分析
Bellman-Ford（分布式、局部信息）
Dijkstra Algorithm（集中式、全局信息）
第一、二、三代互联网路由算法之间的对比和改进

链路代价的计算：决策消耗；信息来源消耗



## 2 Least Cost Algorithms **

slides 20 ~ 

Dijkstra’sAlgorithm （slides 22 ~ 29）：贪心，每次选未加入点中路由代价最小的，然后更新。

可能存在 震荡 问题：zh_CN 247 拥塞敏感，由于链路开销和流量有关，流量不同向时会变化，解决方法有：不同时执行算法。

Bellman-Ford Algorithm （slides30 ~ 36）：拉周围节点更新最短路，开销变小好更新，开销变大会出现routing loop无穷计数。毒性逆转只能解决2两个节点的问题。

Link cost changes：good news fast ， bad news slow （slides37 ~ 38）

difference （slides39 ~ 41）

分类

## 自治系统与路由方式

IRP(IGP) 与 ERP（EGP）概念
内部路由协议
距离向量协议（RIP）与链路状态协议（OSPF）
路由结构图与路由表的生成
BGP
BGP的功能
基本报文类型和工作方式

## IP协议

IP基本原理
异构网络环境下，internet协议的工作过程
协议
协议基本原语与相关参数
IPv4首部格式（各字段含义和变化）

<img src="a%20total%20review.assets/image-20210621210032231.png" style="zoom:33%;" />

IP地址的分类法
A、B、C、D类划分标准和地址范围

- A 0 开始，范围 1 .x.x.x 到 126.x.x.x ，划分是 1 位， 7 位， 24 位
- B 10 开始，范围 128.0.x.x 到 191.255.x.x ，划分是 2 位， 14 位， 16 位 65534
- C 110 开始，范围 192.0.0.x 到 223.255.255.x ，划分是 3 位， 21 位， 8 位 254
- D 1110 开始，代表组播地址

子网划分/聚集
CIDR表达（如12.253.96.0/18）classless interdomain routing



IPv6，和IPv4的异同，优缺点

![](a%20total%20review.assets/image-20210629111804918.png)

---

<img src="a%20total%20review.assets/image-20210621220751867.png" style="zoom:25%;" />

dual-stack 双栈：IPv6/IPv4 节点，都能收发，遗失了部分IPv6特性，比如说flow label field

tunneling 建隧道：两台IPv6间的IPv4路由器集合称为 隧道。IPv6整个作为IPv4的payload

## IP protocol suits

### NAT原理及优缺点

3 Types： static（1-> 1)	dynamic (many --> some) (ip池)  single-Address (many --> 1)端口号

NAT table [ip:port]映射

NAT影响P2P连接，P23：It is not possible to devise such a technique. In order to establish a direct TCP connection between Arnold and Bernard, either Arnold or Bob must initiate a connection to the other. But the NATs covering Arnold and Bob drop SYN packets arriving from the WAN side. Thus neither Arnold nor Bob can initiate a TCP connection to the other if they are both behind NATs.

### ARP地址解析原理和流程

为在同一个子网上的主机和路由器接口解析IP地址。

维护ARP表(有ttl)，根据IP地址查Mac地址。广播帧（ARP request） 

### DHCP动态地址获取的过程

DHCP**获取**：自己的IP地址，子网掩码，本地DNS服务器的IP地址，第一跳默认网关的IP地址

4 step : get yiaddr（your internet address)

- DHCP-discover（**broadcast**）；
- DHCP-offer（each server）；
- DHCP-request（choose one server（**broadcast**）)；
- DHCP-ack(selected server)；host set config with ack
- ...
- DHCP-release

### ICMP：用于发送出错信息，Ping和traceroute的实现原理



ping ：- test dest reachable（echo request[^ICMP type 8 code 0 message]/echo reply[^ICMP type 0 code 0 message]）

traceroute：跟踪 一个主机 到另一个主机 的路由

---

mobile IP：处理移动设备IP地址问题（TCP连接需要固定的destIP)，一个移动实体在移动过程中保持IP地址不变，从应用角度，移动性就变得不可见。

foreign agent作用之一是为 mobile node 初建一个转接地址（COA Care-Of Address）

移动节点得到COA：

归属代理：mobile node告知 归属代理 （home agent）位置

- Discovery
  - mobile agent：ICMP 告知存在
  - mobile node
- Registration
  - mobile node：得到COA,让home agent转发packet过来 mobile <--> froeign agent <--> home agent （request/reply）
  - <img src="a%20total%20review.assets/image-20210622151151386.png" alt="ICMP" style="zoom:23%;" />
- Tunneling

##  IP组播（Multicast）

两个问题：如何识别，如何分发

这个单一标识符。在因特网中，这种表示一组接收方的单一标识就是个D 类多播地址。
与一个D类地址相关联的接收方小组被称为一个 多播组(multicast group)。

---

组播地址、组播模型、组播组管理：IGMP

*组播地址*：D 类 IPv4 地址， 224 开头及往上；组播

<img src="a%20total%20review.assets/image-20210622182300358.png" style="zoom:33%;" />

组播mac地址的高24bit为0x01005e，mac 地址的低23bit为组播ip地址的低23bit。

*组播模型*：主机将 IP 数据报 编址 到 一个 多播组， 路由器 将多播数据报转发给已加入该组播组的主机。

*IP多播路由器*：复制一份（拥有多播功能的路由器），多播responsibilities有(10)有一个守护进程

*组播组管理*：IGMP，host通过ICMP加入多播组[^不包括发送端]，或从中删除

---

组播路由机制：find a spanning tree

Shared-tree, Source-based tree

# 四、传输层

## 传输层服务：

编址、复用、流控制、面向连接、可靠传输

复用：收集不同应用的数据发给网络层

## 可靠传输协议的设计

- 数据包损坏：校验和，ACK，NAK信号
  - ACK有问题就再发一次packet（有seq兜底）
- 数据包丢失：超时计时器
- 按序交付、副本检测：以序列号区分，要求序列号空间足够大
- 传输效率：流水线协议

---

solutions

- Checksums (to detect bit errors)

- Timers (to detect loss)

- Acknowledgements (positive or negative)

- Sequence numbers (to deal with duplicates)


## 流水线协议

### Which packets can sender send?

Sliding window

### How does receiver ack packets?

Cumulative
Selective

### Which packets does sender resend?

Go-Back N (GBN)
Selective Repeat (SR)

---

UDP接收时只负责接收，不用区分发送方（因为UDP协议是无连接的）故使用二元组(目的IP+ 目的端口)；而TCP接收时需要区分发送方(TCP协议是连接的),故四元组(源IP + 源端口 + 目的IP + 目的地址) 

## 传输层协议：UDP，TCP

### UDP协议

无连接、非可靠

## TCP协议

基本服务

---

协议首部格式

<img src="a%20total%20review.assets/image-20210626214049609.png" style="zoom:30%;" />	<img src="a%20total%20review.assets/image-20210626214245215.png" alt="image-20210626214245215" style="zoom:45%;" />

**sequence**：TCP 字节流 所以要 seq number；序号是建立在字节序列上而不是传送报文段的序列上。

**ack**：host A期待从host B收到的下一个字节序列。

---

TCP 仅为传输一次的报文段测量SampleRTT 。无法区分是重传的ACK还是原来的ACK,有二义性【P33】

---

### 流量控制

4-3

1. 滑动窗口机制的设计；发送端[unack ...]；接收端[expect ...];

   [有个二义性问题：接受方可以不发ack实现流控，但是发送方无法确认是丢包还是流控]

2. 信用量窗口 rwnd = buffer size - [已占用大小 recv - read ]

3. TCP复合的窗口管理方式
   - 基于接收方缓冲区
   - 基本机制和工作流程

可能有 接收端在发过W=0后再次打开W=j的包丢失，死锁情况。

---

### 连接维护

#### 连接建立：三次握手

可靠网络与不可靠网络下连接建立与终止的算法对比
三次握手的流程图与其必要性

随机化seq：防止古老的seq到达。<img src="a%20total%20review.assets/image-20210628103622820.png" style="zoom:30%;" />

三方握手：确认对方的SYN和序号

<img src="a%20total%20review.assets/image-20210628103845847.png" alt="image-20210628103845847" style="zoom:33%;" />

SYN/ACK丢包了只能等超时重传，因为SYN/ACK是后面测出RTT(round trip time)的基础，所以这边超时只能根据经验。

#### 连接终止：四次挥手

---

### 拥塞控制算法

IP网络拥塞。端系统发现网络拥塞并处理。（拥塞控制是一个资源分配问题）

发送速率 cwnd/RTT

---

时延RTT估计算法

$$\text{EstimateRTT} = \left( 1 - \alpha
\right)*\text{EstimatedRTT} + \alpha*\text{SampleRTT}$$

$$\text{DevRTT} = \left( 1 - \beta \right)*\text{DevRTT} +
\beta*\left| \text{SampleRTT} - \text{EstimatedRTT} \right|$$

RTO计时器管理算法$$\text{RTO}\left( k + 1 \right) =
\text{Min}(\text{UBOUND},\text{MAX}\left(
\text{LBOUND},\beta*\text{SRT}T\left( k + 1 \right)) \right))$$

---

Jacobson’s Reno

毙掉的方案：不管，资源预留，竞价（不公平）

- 慢启动（Linear increase per ACK(CWND+1)==-->== exponential increase per RTT (2*CWND) ）

  - cwnd(Congestion Window)的值设置为**1个MSS**(maximum segment size)的较小值
  - cwnd的值以1个MSS开始，每当传输的报文段首次被确认就增加1个MSS（事实上是在翻倍）

  - 何时结束

    -   存在一个由超时指示的丢包（即拥塞）

        -   将ssthresh（慢启动阈值）设置为cwnd/2

        -   将cwnd设置为1并重新开始慢启动

    -   cwnd的值等于ssthresh时

        -   结束慢启动并进行**拥塞避免**模式

    -   检测到3个冗余ACK

        -   执行**快速重传**并进入快速回复状态

- 拥塞避免：窗口增长基本算法（AIMD）

  <img src="a%20total%20review.assets/image-20210628164714037.png" style="zoom:30%;" />

  -   此时cwnd的值大约时上次遇到拥塞时的一半

  -   每个RTT只讲cwnd的值增加一个MSS

      -   每个到达ACK增加MSS/cwnd字节的cwnd

  -   何时结束

      -   超时：与慢启动相同

      -   3个冗余ACK

          -   将ssthresh的值记录为cwnd的值的一半

          -   cwnd的值减半

          -   进入快速恢复状态

- 快重传

  -   触发条件：TCP发送方接收到对相同数据的3个冗余ACK
  -   说明这个已被确认过3次的报文段之后的报文段已经丢失

---

快恢复

-   cwnd设置为上一个阈值+1

-   进入拥塞避免状态

##  数据网络中的拥塞控制

拥塞问题
网络拥塞和性能指标
拥塞情况下网络吞吐率特征

### 拥塞控制方式

-   抑制分组（拥塞分组）control packet ==ICMP==

    -   generated at congested node

    -   send to source node
-   反压（逐跳）hop-by hop choke packet [长距离]
-   警告位 warning bit

    -   special bits set in the packet header by switch
    -   取消了二义性
-   随机早期丢弃（RED）
-   公平队列：轮询，大小流互不干扰

# 五、网络安全

RSA算法

报文完整性：数字签名；端点鉴别【源自Alice，没有被篡改】

m, H(m+s)