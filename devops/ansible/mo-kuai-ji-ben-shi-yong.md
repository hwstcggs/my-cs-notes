# 简介

通过命令行来执行三个不同的模块:

```
ansible webservers -m service -a "name=httpd state=started"
ansible webservers -m ping
ansible webservers -m command -a "/sbin/reboot -t now"
```

每个模块都能接收参数. 几乎所有的模块都接受键值对\(`key=value`\)参数,空格分隔.一些模块 不接收参数,只需在命令行输入相关的命令就能调用

在 playbook 中, Ansible 模块以类似的方式执行:

```
- name: reboot the servers
  action: command /sbin/reboot -t now
```

也可以简写成:

```
- name: reboot the servers
  command: /sbin/reboot -t now
```

另一种给模块传递参数的方式是使用 ymal 语法,这也被称为 ‘complex args’

```
- name: restart webserver
  service:
    name: httpd
    state: restarted
```

无论你是使用命令行还是 playbooks 所有模块都会返回以 JSON 格式组织的数据.一般来说,对此你 无需知道太多.但如果你在编写你自己的模块,那你需要在意,这意味着你不需要以特定的语言来编写 你的模块 – 你可以自行选择.

模块努力使自身幂等,这意味着它们会尽可能避免对系统做出改动除非那是必须的.当使用 Ansible playbooks 时,这些模块能够触发 ‘change events’,以这种形式通知 ‘handlers’ 去运行附加任务.

每个模块的文档能够通过命令行的 ansible-doc 工具来获取:

```
ansible-doc yum
```

列出所有已安装的模块文档:

```
ansible-doc -l
```

## 模块命令

```
-i 设备列表路径，可以指定一些动态路径
-f 并发任务数
-private-key 私钥路径
-m 模块名称
-M 模块夹的路径
-a 参数
-k 登陆密码
-K sudo密码
-t 输出结果保存路径
-B 后台运行超时时间
-P 调查后台程序时间
-u 执行用户
-U sudo用户
-l 限制设备范围
-s 是此用户sudo无需输入密码
```

## copy模块

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



## file模块

  


