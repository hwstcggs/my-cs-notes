## ping模块

\#使用ansible的ping模块测试client是否能够通信！

```
#注意：all 代表所有client的意思
[root@ansibleserver ~]# ansible all -m ping

192.168.1.232 | success >>{
"changed":false, 
"ping":"pong"
}

127.0.0.1 | success >>{
"changed": false,     
"ping":"pong"
}

#查看时间
[root@ansibleserver ~]# ansible all -m command -a "date"

192.168.1.232 | success | rc=0 >>
Tue Mar 17 23:06:43 EDT 2015

127.0.0.1 | success | rc=0 >>
Tue Mar 17 23:06:44 EDT 2015
```



