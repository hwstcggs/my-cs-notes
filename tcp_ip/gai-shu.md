传入一个IP或者一个主机名作为参数，发送一个ICMP响应请求，然后显示返回包完整的构造

```
import sys
from scapy.all import sr1,IP,ICMP

p=sr1(IP(dst=sys.argv[1])/ICMP())
if p:
    p.show()
```



