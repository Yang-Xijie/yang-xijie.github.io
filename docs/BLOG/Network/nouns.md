# 计算机网络 专有名词速查

> 2021年秋季学期 计算机网络 李风华 清华大学
> 
> 无97 杨希杰 总结笔记

## 1 概论

- ARPA计算机计划：Advanced Research Project Agency
- ARPANET：Advanced Research Project Agency net
- CERNET：
- FITI：Future Internet Technology Infrastructure

---

- LAN：局域网
- Ethernet：以太网
- WLAN：Wireless LAN 无线局域网
- MAN：城域网
- WAN：广域网
- PAN：个域网

## 2 计算机网络体系结构

- 服务访问点SAP: Service Access Point 
- 接口数据单元IDU: Interface Data Unit 
- 服务数据单元SDU(Service Data Unit)
- 接口控制信息ICI(Interface Control Information)
- 协议数据单元PDU(Protocol Data Unit)
- 协议控制信息PCI (Protocol Control Information)
- 国际电信联盟ITU(International Telecommunication Union)
- 国际标准化组织ISO(International Standards Organization)
- 国际标准IS(International Standard)

---

- ANSI:美国国家标准协会，ISO的美国代表
- NIST:美国国家标准和技术协会，美国商业部的标准化组织
- IEEE:电子和电器工程师协会，发布行业标准
- CCSA:中国通信标准化协会，发布行业标准

---

- Internet的标准 RFC(Request for Comment)
- OSI(Open System Interconnection)参考模型
- 逻辑链路控制LLC(Logical Link Control)
- 介质访问控制MAC(Media Access Control)

---

- bit：比特
- frame：帧
- package：分组
- segment：段

---

- tcpdump：某网络分析工具

## 3 物理层技术

- 有限带宽信号(Bandwidth Limited Signals)
- 频谱(spectrum)
- 带宽(bandwidth)
- 波特率(baud)每秒钟信号变化的次数，也称调制速率。
- 不归零制码(NRZ:Non-Return to Zero)

---

- 调制(Modulation)
- 解调(Demodulation):调制的反变换。
- 调制解调器MODEM(modulation-demodulation)
- 幅移键控法(调幅) Amplitude-shift keying (ASK)
- 频移键控法 (调频)Frequency-shift keying (FSK)
- 相移键控法(调相) Phase-shift keying (PSK)

---

- 时分复用 TDM(Time Division Multiplexing)
- 频分复用 FDM(Frequency Division Multiplexing)
- 波分复用 WDM(Wavelength Division Multiplexing)

---

- 电路交换(circuit switching)
- 报文交换(message switching)
- 分组交换(packet switching)
- 数据报(datagram)
- 虚电路(virtual circuit)

## 4 数据链路层技术 1

- 海明码
- 循环冗余码(CRC码，多项式编码)

## 5 数据链路层技术 2

- 载波监听多路访问协议CSMA(Carrier Sense Multiple Access Protocols)
- 逻辑链路控制子层LLC(Logical Link Control)
- 介质访问控制子层MAC(Medium Access Control)

## 6 网络层技术 1

- TTL: 生存期(Time to live)
- 无类域间路由CIDR(Classless InterDomain Routing)
- Internet控制消息协议ICMP(Internet Control Message Protocol)
- 地址解析协议ARP(Address Resolution Protocol)
- 反向地址解析协议RARP(Reverse Address Resolution Protocol)

## 7 网络层技术 2

- RIP: Routing Information Protocol 路由信息协议（域内路由协议 典型的距离向量路由协议）
- OSPF: Open Shortest Path First 开放的最短路径优先协议（域内路由协议 典型的链路状态路由协议）

## 8 网络层技术 3

- 边界网关协议BGP(Border Gateway Protocol)

## 9 传输层技术 1

- TPDU: Transport Protocol Data Unit，是指传送协议数据单元
- 传输服务访问点TSAP(Transport Service Access Point)
- 传输控制协议TCP(Transmission Control Protocol)
- 用户数据报协议UDP(User Datagram Protocol)
- RTT(Round Trip Time)：单位往返周期
- 拥塞窗口(Cwnd:Congestion Window)
- 可变发送窗口(Awnd:Advertised Window)
- AIMD(Additive Increase / Multiplicative Decrease)

## 10 应用层技术

- IPS(Interprocess Communication)
- API(Application Programming Interface)
- DNS(Domain Name Service)
- WWW(World Wode Web)
- HTML(Hyper Text Markup Language)
- P2P(Peer-to-peer)
