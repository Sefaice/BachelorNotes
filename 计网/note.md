## chapter1

process delay，transmission delay，propagation delay，queuing delay

数据在不同层：message，segment，datagram，frame

## chapter2

sockets

HTTP：cookies，持续和非持续

FTP：两个TCP连接

SMTP：delivery/storage to receiver’s server，只到receiver’s server，负责从receiver’s server到receiver的有：POP3/IMAP/HTTP。SMTP和HTTP对比（P148）

**DNS****: domain name system，基于UDP，prot53

BitTorrent：P2P协议

## chapter3

transport layer in contrast with network layer: network laye - logical communication between hosts, transport layer - logical communication between processes (书P222)

multiplexing and demultiplexing

UDP

principles of reliable data transfer：rdt - GoBackN/selective repeat

### TCP

data transfer：只ACK确定的下一位数据；fast retransmit：3个同样的ACK，立即重传。采用GoBackN。MSS与MTU 

flow control：avoid sender overflowing receiver’s buffer

connection management：三次握手，四次挥手

congestion control：避免网络阻塞，和flow control区分。算法。

## chapter4

vc有连接，datagram无连接，和传输层有连接无连接区别

router和fowarding

inside a router：switch fabric - input和output都有可能buffer

IP: FRAGMENTATION, DHCP, NAT, ICMP

路由算法：ls和dv

RIP: UDP，dv，发给邻居

OSPF：ls，广播给所有节点

BGP：TCP

## chapter5

CRC

MAC协议

MAC地址和ARP