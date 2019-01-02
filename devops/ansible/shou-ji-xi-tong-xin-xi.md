## 收集系统信息

```
#收集主机的所有系统信息
[root@ansibleserver ~]# ansible 192.168.1.232 -m setup

#收集系统信息并以主机名为文件名分别保存在/tmp/facts目录
[root@ansibleserver facts]# ansible 192.168.1.232 -m setup --tree/tmp/facts
[root@ansibleserver facts]# ll
total 12
-rw-r--r-- 1 root root 8656 Mar 18 00:25 192.168.1.232

#收集系统内存相关信息
[root@ansibleserver ~]# ansible 192.168.1.232 -m setup -a'filter=ansible_*_mb'
192.168.1.232 | success >> {
    "ansible_facts": {
       "ansible_memfree_mb": 299, 
       "ansible_memtotal_mb": 490, 
       "ansible_swapfree_mb": 2047, 
       "ansible_swaptotal_mb": 2047
    }, 
    "changed": false
}

#收集网卡信息
[root@ansibleserver ~]# ansible 192.168.1.232 -m setup -a'filter=ansible_eth[0-2]'

```



