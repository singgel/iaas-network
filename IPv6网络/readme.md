# 名次解释

**熟悉这些名词有助于在交流过程中知道双方讨论的是什么**

路由通告报文RA（Router Advertisement）

身份联盟IA（Identity Association）

路由请求报文RS（RouterSolicitation）

路由通告报文RA（Router Advertisement）

邻居请求报文NS（Neighbor Solicitation）

邻居通告报文NA（NeighborAdvertisement）

# IPv6的特殊地址

**熟悉这些特殊地址有助于在抓包过程中知道client发起请求的目的是做什么**

## DHCP使用的地址

在DHCPv4协议中，客户端发送广播报文来定位服务器。为避免广播风暴，在IPv6中，已经没有了广播类型的报文，而是采用组播报文。DHCPv6用到的组播地址有两个：

-   FF02::1:2（All DHCP Relay Agents and Servers）：所有DHCPv6服务器和中继代理的组播地址，这个地址是链路范围的，用于客户端和相邻的服务器及中继代理之间通信。所有DHCPv6服务器和中继代理都是该组的成员。
-   FF05::1:3（All DHCP Servers）：所有DHCPv6服务器组播地址，这个地址是站点范围的，用于中继代理和服务器之间的通信，站点内的所有DHCPv6服务器都是此组的成员。

![]()

## 组播使用的地址

**这里的组播地址跟上面的DHCP6的组播地址还不一样，通过特殊地址列表可以快速在抓包报文中分析问题**

组播地址，是预留的特殊用途的组播地址。

| 地址      | 应用                 |
| ------- | ------------------ |
| FF01::1 | 表示节点本地范围所有节点的组播地址  |
| FF02::1 | 表示链路本地范围所有节点的组播地址  |
| FF01::2 | 表示节点本地范围所有路由器的组播地址 |
| FF02::2 | 表示链路本地范围所有路由器的组播地址 |

另外，还有一类组播地址：被请求节点（Solicited-Node）地址。该地址主要用于获取同一链路上邻居节点的链路层地址及实现重复地址检测。每一个单播或任播IPv6地址都有一个对应的被请求节点地址。其格式为：

FF02:0:0:0:0:1:FFXX:XXXX

其中，FF02:0:0:0:0:1:FF为104位固定格式；XX:XXXX为单播或任播IPv6地址的后24位。

## 其他特殊地址

FF02::1 所有结点地址，用于到达同一个链接上的所有结点

FF02::2 所有路由器地址，用于到达同一个链接上的所有路由器

FF02::4 所有“距离矢量组播路由协议(DVMRP)”路由器地址，用于到达同一个链接上的所有DVMRP组播路由器

FF02::5 所有“开放式最短路径优先(OSPF)”路由器地址，用于到达同一个链接上的所有OSPF路由器

FF02::6 所有指派的(OSPF)路由器地址，用于到达同一个链接上的所有指派的OSPF路由器

FF02::6 在本地链路起作用，代表所有的RIP路由器 

FF02::16

![]()

FF02::1:FFXX：XXXX 请求结点地址，用在地址解析过程中，以便将链接本地结点的IPv6地址解析为它的链接层地址。

                            请求结点地址的最后24位(XX:XXXX)是IPv6单播地址的最后24位

FF02::1:FF4C:0 被请求节点组播地址，路由器会监听所有这些地址，用于DAD冲突检测和邻居请求，响应查询信息

# IPv6的DHCP6

**熟悉DHCP6有助于排查在虚拟机的port网卡地址分配和交互内容问题，这些影响着数据面的行为**

## DHCPv6 SDN控制面用到的option

![]()

## DHCPv6 SDN控制面用到的status code

![]()

## DHCPv6与DHCPv4

![]()

# IPv6的ND

**熟悉ND有助于排查在IPv6的链路中出现的网络可达性问题，这些影响着流量的行为**

**例如：**

**ARP由NS/NA替换实现：地址解析/重复地址检测**

## 邻居发现协议作用

1.  IPv6邻居发现使用的ICMPv6消息
1.  地址解析
1.  验证邻居是否可达
1.  重复地址检测
1.  路由器发现/前缀发现及地址无状态自动配置
1.  重定向功能
1.  协议规范

![]()

# Linux相关工具介绍：

nmcli工具：

<https://www.cnblogs.com/liuhedong/p/10695969.html>

# 参考链接：

RFC：

<https://rfc2cn.com/rfc3315.html>

<https://rfc2cn.com/rfc8415.html>

<https://rfc2cn.com/rfc2461.html>

·     RFC 1881：IPv6 Address Allocation Management

·     RFC 1887：An Architecture for IPv6 Unicast Address Allocation

·     RFC 1981：Path MTU Discovery for IP version 6

·     RFC 2375：IPv6 Multicast Address Assignments

·     RFC 2460：Internet Protocol, Version 6 (IPv6) Specification

·     RFC 2464：Transmission of IPv6 Packets over Ethernet Networks

·     RFC 2526：Reserved IPv6 Subnet Anycast Addresses

·     RFC 3307：Allocation Guidelines for IPv6 Multicast Addresses

·     RFC 4191：Default Router Preferences and More-Specific Routes

·     RFC 4291：IP Version 6 Addressing Architecture

·     RFC 4443：Internet Control Message Protocol (ICMPv6) for the Internet Protocol Version 6 (IPv6) Specification

·     RFC 4861：Neighbor Discovery for IP Version 6 (IPv6)

·     RFC 4862：IPv6 Stateless Address Autoconfiguration



华三：

<https://www.h3c.com/cn/d_202209/1692790_30005_0.htm>

华为：

<https://support.huawei.com/enterprise/zh/doc/EDOC1100116138>

思科：<https://community.cisco.com/t5/%E7%BD%91%E7%BB%9C%E6%96%87%E6%A1%A3/%E5%8E%9F%E5%88%9B-dhcpv6-%E8%AF%A6%E6%83%85%E5%8F%8A%E5%85%B6%E6%8A%A5%E6%96%87%E4%BB%8B%E7%BB%8D-%E9%99%84%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B%E5%8F%8A%E9%AA%8C%E8%AF%81%E5%91%BD%E4%BB%A4/ta-p/4372251>