## 服务管理

```
#启动client的httpd服务
[root@ansibleserver ~]# ansible 192.168.1.232 -m service -a"name=httpd state=started"
192.168.1.232 | success >> {
    "changed": true, 
    "name":"httpd", 
    "state":"started"
}
#注意：state的状态有：started   restarted   stoped
#client端查看情况
[root@localhost ~]# netstat -lntup|grep httpd
tcp        0      0 :::80                       :::*                        LISTEN      1565/httpd

```



