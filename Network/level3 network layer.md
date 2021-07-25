# 网络层

$$
Network\ \ layer\begin{cases}
IP \ \ protocol&
\\\\
routing \ \ protocol&\\\\ 
ICMP (Internet \ Control\ Message\ Protocol)&
\end{cases}
$$

CH-3 slides51 Summary of Header Changes (IPv4 --> IPv6)

# lesson 1 网络层功能 router VC数据报网络

## Intro 

slides 4 ~ 7  （2 functions）

①交换/路由；②转发	路由决定了转发表

slides 8 ~ 11 （连接建立 网络服务模型）

## IP Routers

slides 13 ~ 17

router capacity = N(ports) * R(link rate[speed])

router 路由器的构成 ：①跑路由算法；②转发

slides 18 ~ 28 (Input Port)

找端口号用前缀匹配；主要挑战是处理速度（更新表头）

slides 29 ~ 34 (Output Port)

①packet 分组；②buffer 管理；③调度

slides 35 ~ 39 (Connecting inputs to outputs)

shared memory；bus；inter-connection network

## Virtual Circuit and Datagram Networks

# lesson 2 IP协议 地址

## Intro

slides 3 ~ 5

## Internet Addressing

slides 7 ~ 10 编址规则 addressing conventions

address level：二层地址，三层地址（全球可达），五层地址（区分应用）

## IP Operations 

slides 12 ~ 18

- Routing：主机和路由器维护路由表
- Datagram lifetime: ttl 保证不出现环路情况
- Fragmentation and re-assembly：分片重组，router高速转发
- Error control：ICMP
- Flow control

## IP Packet Structure

slides 20 ~ 25

## Dealing with Fragmentation

slides 27 ~ 36

### IP Address

slides 38 ~ 53

> en P338: an IP address is technically associated with an interface[^int]
>
> ch P225: IP 要求每台主机 和 路由器**接口**拥有自己的 IP 地址。
>
> [^int]: The boundary between the host and the physical link is called an interface.

IP地址【全球唯一】

Network part (high order bits)：全0和全1的地址要扣除，全0是网络号，全1是广播号

# lesson 3 NAT ICMP

## NAT

slides 3 ~ 8 network address translation

3 Types： static（1-> 1)	dynamic (many --> some) (ip池)  single-Address (many --> 1)端口号

---
实现方式： NAT table

IP protocol suits

## ICMP

slides 10 ~ 17

IP协议 主流程 ICMP控制问题：排错\&管理

## Mobile IP

slides 19 ~ 25

### The Protocol

slides 26 ~ 34

Discovery：知道支持

Registration：

Tunneling：

## IPv6

slides 36 ~ 54

RFC (Request For Comments)

快速处理IP 分组是处理的焦点

# lesson 4 routing

路由，效率，弹性，稳定

集中式路由
分布式路由：洪泛，随机行走，自适应路由
最小代价路由算法及其性能分析
	DijkstraAlgorithm（集中式、全局信息）
	Bellman-Ford（分布式、局部信息）
链路代价的计算

## Routing

slides 4 ~ 9

Routing （slides 6 ~ 9）  

性能指标：怎么定义 cost ；决策消耗；信息来源消耗

Routing Strategies （slides 10 ~ 19）

## 2 Least Cost Algorithms **

slides 20 ~ 

Dijkstra’sAlgorithm （slides 22 ~ 29）：贪心，每次选未加入点中路由代价最小的，然后更新。

可能存在 震荡 问题：zh_CN 247 拥塞敏感，由于链路开销和流量有关，流量不同向时会变化，解决方法有：不同时执行算法。

Bellman-Ford Algorithm （slides30 ~ 36）：拉周围节点更新最短路，开销变小好更新，开销变大会出现routing loop无穷计数。毒性逆转只能解决2两个节点的问题。

Link cost changes：good news fast ， bad news slow （slides37 ~ 38）

difference （slides39 ~ 41）

分类

# lesson 5 as routing

层次结构的routing，AS内部路由，AS间外部路由，分界处称为gateway，内外协议分别就是IGP(RIP,OSPF) 和EGP:(BGP)

slides 13 ~ 15：第一代DistanceVector（局部）：毒性逆转 --> 第二代LinkState（全局）

EGP：两个基础的路由选择算法都不够满足要求

## RIP vs OSPF

slides 21~ 24  zh_CN 258 en_US 384	路由选择信息协议 Routing InformationProtocol (RIP) 

slides 25~ 36	

SPF（short path first) tree

最显著advanced ：OSPF Areas （35）层次式路由；其他诸如安全，多路使用，单播广播（33，zh_CN 261）

slides 37 RIP vsOSPF

##  BGP 域间路由 [^179tcp]

Border Gateway Protocol

slides 39 ~ 44 : AS topo 反应了AS间的商业关系

slides 45~ 53：DV改进：目的地是子网前缀，不一定选最短路，path vector(避免环路) ，不保证可到达，聚合前缀路由

## eBGP, iBGP, and IGP

slides 55 ~ 60  BGP细节	speak BGP slide-56

slides 61 ~ 69 Basic messages in BGP，Specifies what messages to exchange with other BGP “speakers”

slides 63 ~ 67	Route attributes

# lesson 6 IP multicasting

## Basic of IP Multicast

slides 5 ~ 6 concepts；slides 7 ~ 9  IP Multicast

slides 10 ~ 11 Multicast Router Responsibilities

slides 13 **IP Multicast Architecture**

slides 14 ~ 16 Service Model：主机host把 IP数据包发给一个多播分组，然后路由器再分发给多播分组（注意下地址转换）

## IGMP: Internet Group Management Protocol

slides 18~19 IGMP：Host <---> router 交换多播组的信息

slides 20 ~ 22 Operations；slides 23 ~ 25 IGMP Versions #TODO

slides 26 ~ 34 Membership Query

## Multicast Routing

slides 36 Multicast Routing

连接组成员的spanning tree，shared tree（全部一样）和 source tree（各个节点不同）

## Application-level Multicast

slides 48 



