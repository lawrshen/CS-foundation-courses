#  lesson 1 链路层服务

1.成帧(9)；2.链路接入(10-12)；3.可靠性传输(**13-18**)；4.错误校验和纠错(奇偶，checksum(16bits求和的反码作为校验码，全0不要校验码UDP 135) zn_ch 295，CRC)

3，4 layer 流控

![](level2 link layer.assets\image-20210618194242598.png)

## 错误检测：奇偶校验，CRC的计算

格式为

```
+-——————-——+----------+
|			数据	D		 | 校验码 R |
+-——————-——+----------+
```

d+r 位，R 冗余校验码，判断标准是 D,R 整除 G

Since $𝐷∗2^𝑟$=𝑎∗𝐺⊕𝑅, so $𝐷∗2^𝑟⊕𝑅$=𝑎∗𝐺
Obtain R by:
$$
R=remainder[\frac{D\cdot 2^r}{G}]
$$

被发送的数据： $D\cdot 2^r\; \text{XOR} \;R$ d+r 比特 (D G -->R,G是生成多项式)

## 流控制：Stop and Wait，Sliding Window

flow control : reliable delivery

Sliding Window  : GBN (go back n)硬件实现简单，selective reject

## 局域网 LAN

### 令牌环

### 以太网

Ethernet: unreliable, connectionless

#### 以太网帧格式

Preamble  |  DstAddress  |  SourceAddress  | type  |  		 Data		  |   CRC

(7+1)byte  |  		6	 		|		 	6				|	2	|		46~1500	  |	 4

前同步码

# 	lesson 2 Multiple access control

> 多路访问问题（multiple access problem）：如何协调多个发送和接收节点对一个共享广播信道的访问？

- 多路访问协议（multiple access protocol）：节点通过这些协议来规范它们在共享的广播信道上的传输行为。
- 碰撞（collide）：多个节点同时传输帧，所有节点同时接到多个帧，没有一个节点能够有效的获得任何传输的帧。

理想情况下MAC所期待的四种特性：

- 单个节点具有全部吞吐量（R bps）
- 多个节点均分共享吞吐量（R/M bps)
- 协议是分布式的，没有特殊节点负责转发，没有同时的时钟和槽
- 简单

### 信道切分

时分；频分；码分

### 轮流访问

master；distributed

### 随机访问

## CSMA (载波侦听多路访问)

Carrier sense multiple access (载波侦听多路访问)
### Nonpersistent，1-persistent，p-persistent

### CSMA/CD原理，算法（IEEE 802.3，以太网）

# lesson 3 utilization ARP DHCP

随机访问接入的性能

## ARP & DHCP

DNS为Internet任何地方的host解析主机名，而ARP只为在同一个子网上的主机和路由器接口解析IP地址。

# lesson 4 Bridge and Layer 2 Switch

## 概念

连接局域网LANs

1. 选择性存储 转发
2. 透明
3. 即插即用 自学习

广播机制

## 广播风暴问题

拓扑有环

## 生成树算法

选root && 最短路（lower ID)

Message(Y, d, X) Y: root ,d: distance to Y, X: node X

鲁棒性：节点（root和其他）的崩溃	root周期发报文，超时其他节点重新claim root

## 地址学习机制

减少广播的浪费，switch table存储来的节点address和端口port

> 二层交换机 记录传来的link，MAC address 更新switch table，entry for destination

# lesson 5 Wireless Networks

Elements of a wireless network: wireless hosts, base station, wireless link

无线网络两种模式：与基站关联的主机：**基础设施模式**（Infrastructure mode), 和Ad-hoc mode（自组织 known）

Wireless link characteristics：

- Decreased signal strength: Radio signal attenuates as it propagates through matter (path loss)：平方衰减：频率越高，波长越小，衰减越快
- Multipath propagation: Radio signal reflects off objects ground, arriving ad destination at slightly different times
- Interference from other sources: Standardized wireless network frequencies (e.g., 2.4 GHz) shared by other devices (e.g., phone); devices (motors) interfere as well：其他干扰

WiFi 802.11:

802.11架构：AP BSS -- DS -- ESS     --（portal）--> LAN         

---

association	slides 28 - zh_CN 367；us_en 594

---

信道划分，multiple access： Hidden terminal 终端隐藏； Signal fading 信号衰弱； Exposed terminal problem 暴露终端问题，信号损失

802.11的MAC协议：CSMA/CA，不同于CSMA/CD ，无线不好做碰撞检测，使用了碰撞避免（collision avoidance）slides 41 ；zh_CN 368；us_en 595             

liink-layer ack: RTS CTS zh_CN 370 链路层确认 4个帧交互，浪费带宽先做一次交换

三种优先级slides

---

802.11	frame                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

主要区别是4个mac地址，第四个是ad-hoc mode，前三个：

接收帧的地址	<-->	发送帧的设备（host 或者AP）	<-->	连接到其它网络的路由器端口

> IEEE 802.11数据帧有四种子类型，分别是IBSS、From AP、To AP、WDS。这里的数据帧F是从笔记本电脑发送往访问接入点（AP），所以属于To AP子类型。这种帧地址1是RA（BSSID），地址2是SA，地址3是DA。RA是receiver address的缩写，BSSID是basic service set identifier的缩写，SA是source address的缩写，DA是destination address的缩写。因此地址1是AP的MAC，地址2是H的MAC，地址3是R的MAC， [试题](https://www.nowcoder.com/profile/842680558/test/44865122/160058#summary)。

AP到router，最后一跳，有线网扩展到无线网。

---

advanced	slides 50 ；zh_CN 374；us_en 605     

rate adaptation；power management(省电)