# Transport layer basics

服务模型：提供逻辑通信，运行在端系统上。

多路复用和解复用 slides6 ； 14

Role of the transport layer  slides 7 ~ 11 提供进程通信，可靠传输（optional）

socket port  slides13 ~ 14

主机host上每个套接字socket分配了一个端口号port，当报文段到达主机时，运输层检查报文段的目的端口号，并定向至对应的socket。

# UDP & TCP

UDP slides 4 ~ 10	7：Segment Format
TCP slides 12

Retransmission timeout  slides 34

# TCP 流控 拥塞控制

flow control slides 4 ~ 18

# TCP不足 router辅助

TCP congestion control wrap-up

TCP throughput equation

Problems with congestion control

Router assisted congestion control slides

