## file模块

  
\#使用file模块，更改文件的用户和权限

```
[root@ansibleserver ~]# ansible 192.168.1.232 -m file -a "dest=/tmp/a.txtmode=600"
#查看更改情况
[root@localhost tmp]# ll
total 8
-rw-------  1 root root    0 Mar 17 23:38 a.txt

#创建目录，类似mkdir –p
[root@ansibleserver ~]# ansible 192.168.1.232 -m file -a "dest=/tmp/to/c mode=755 owner=root group=root state=directory"
#查看创建情况
[root@localhost c]
# pwd
/tmp/to/c

#删除文件或者目录
[root@ansibleserver ~]
# ansible 192.168.1.232 -m file -a"dest=/tmp/a.txt state=absent"

192.168.1.232 |success >>{
"changed":true, 
"path":"/tmp/a.txt", 
"state":"absent"
}

#查看删除情况
[root@localhost tmp]
# ll
total 8
-rw-r--r--  1 root root    0 Mar 17 23:38 b.txt
drwxr-xr-x  2 root root 4096 Mar 1723:38 script
drwxr-xr-x  3 root root 4096 Mar 1723:53 to
-rw-------. 1 root root    0 Dec 2819:45 yum.log
```



