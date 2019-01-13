# ARP - 地址解析协议

用于以太网的ARP请求或应答分组格式

![](/tcp_ip/images/arp-01.jpeg)

特殊ARP

- 免费ARP （Gratuitous ARP）

 - 宣告广播的作用，以告诉整个广播域，目前这个IP所对应的MAC地址是什么（网络设备冷备）
 - 看看广播域内有没有别的主机使用自己的IP，如果使用了，则在界面上弹出“IP冲突”字样（防止地址冲突）

- 代理ARP （Proxy ARP）
 -  正面意义
  - nat
 - 

