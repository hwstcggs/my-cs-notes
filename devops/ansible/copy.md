# copy模块

```
#拷贝文件到远程主机
相关选项如下：
backup：在覆盖之前，将源文件备份，备份文件包含时间信息。有两个选项：yes|no
content：用于替代“src”，可以直接设定指定文件的值
dest：必选项。要将源文件复制到的远程主机的绝对路径，如果源文件是一个目录，那么该路径也必须是个目录
directory_mode：递归设定目录的权限，默认为系统默认权限
force：如果目标主机包含该文件，但内容不同，如果设置为yes，则强制覆盖，如果为no，
       则只有当目标主机的目标位置不存在该文件时，才复制。默认为yes
others：所有的file模块里的选项都可以在这里使用
src：被复制到远程主机的本地文件，可以是绝对路径，也可以是相对路径。如果路径是一个目录，
    它将递归复制。在这种情况下，如果路径使用“/”来结尾，则只复制目录里的内容，如果没有使用“/”来结尾，
    则包含目录在内的整个内容全部复制，类似于rsync。
```

```
实例：拷贝本地的/root/script目录所有内容到192.168.1.232的/tmp目录下
注意：因为script后面没有加/ ，所以拷贝的是整个目录
ansible 192.168.1.232 -m copy -a "src=/root/script dest=/tmp/owner=root group=root mode=0644"
#拷贝成功的返回信息
192.168.1.232 | success >> {
   "changed": true, 
   "dest": "/tmp/", 
   "src": "/root/script"
}

#切换到192.168.1.232机器中查看
[root@localhost ~]# ls /tmp/script/
a.txt  b.txt
#拷贝script目录的文件实例：
注意：这里的script后面是加了/ ，所以只拷贝script目录下的文件
[root@ansibleserver script]# ansible 192.168.1.232 -m copy -a"src=/root/script/ dest=/tmp/script/ owner=root group=root mode=0644"
192.168.1.232 | success >> {
    "changed": true, 
    "dest":"/tmp/script/", 
    "src":"/root/script"
}
```

```
在192.168.1.232的script目录下查看内容
[root@localhost script]# ll
total 0
-rw-r--r-- 1 root root 0 Mar 17 23:38 a.txt
-rw-r--r-- 1 root root 0 Mar 17 23:38 b.txt
-rw-r--r-- 1 root root 0 Mar 1723:38 c.txt
-rw-r--r-- 1 root root 0 Mar 1723:38 d.txt
#backup参数：有yes|no两个选项
ansible 192.168.1.232 -m copy -a "src=/root/script/ dest=/tmp/script/owner=root group=root mode=0644 backup=yes"
提示：例如，src和dest同时有个a.txt文件，如果在src修改了a.txt  再执行copy的时候，dest就会生成一个备份

[root@localhost script]# ll
total 4
-rw-r--r-- 1 root root 12 Mar 18 03:09 a.txt
-rw-r--r-- 1 root root  0 Mar 18 03:08 a.txt.2015-03-18@03:09~ 
#因为a.txt被修改过了，所以生成了一个备份

[root@localhost script]# cat a.txt  #这里被修改过，然后copy过来的
hello world
[root@localhost script]# cat a.txt.2015-03-18\@03\:09~ #备份的a.txt默认没有内容
```



