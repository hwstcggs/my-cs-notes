## synchronize模块

```
#先声明下，使用rsync 模块，远程主机系统必须安装rsync 包，否则无法使用这个模块
#先给远程机装个rsync吧

[root@ansibleserver ~]# ansible 192.168.1.232 -m yum -a 'name=rsyncstate=latest'

#再次验证下rsync是否安装成功
[root@ansibleserver ~]# ansible 192.168.1.232 -a "which rsync"
192.168.1.232 | success | rc=0 >>
/usr/bin/rsync
#看来没问题了！
```

```
#看下使用的参数
[root@ansibleserver ~]# ansible-doc -s synchronize
- name: Uses rsync to make synchronizing file paths in your playbooks quickand easy.
action: synchronize
archive                # 是否采用归档模式同步，即以源文件相同属性同步到目标地址
checksum               # 是否效验
compress               # 是否压缩
copy_links             # 同步的时候是否复制连接
delete                 # 删除源中没有而目标存在的文件
dest=                  # 目标地址
dest_port              # 目标接受的端口
dirs                   # 以非递归的方式传输目录
existing_only          # Skipcreating new files on receiver.
group                  # Preservegroup
links                  # Copysymlinks as symlinks.
mode                   # 模式，rsync 同步的方式 PUSH\PULL
recursive              # 是否递归 yes/no
rsync_opts             # 使用rsync 的参数
rsync_path             # 服务的路径（源码编译时需指定）
rsync_timeout          # Specify a--timeout for the rsync command in seconds.
set_remote_user        # put user@for the remote paths. If you have a custom ssh config to define the remote userfor
src=                   # 源，同步的数据源
times
```

```
实例：将ansible端/tmp/目录下的script同步到232机子的/tmp/目录下面
[root@ansibleserver ~]# ansible 192.168.1.232 -m synchronize -a 'src=/tmp/script dest=/tmp/' 
192.168.1.232 | success >> {
    "changed": true, 
    "cmd": "rsync--delay-updates -FF --compress --archive --rsh 'ssh  -o StrictHostKeyChecking=no'--out-format='<<CHANGED>>%i %n%L' \"/tmp/script\"\"root@192.168.1.232:/tmp/\"", 
    "msg":"cd+++++++++ script/\n<f+++++++++ script/a.txt\n", 
    "rc": 0, 
    "stdout_lines": [
        "cd+++++++++script/", 
        "<f+++++++++script/a.txt"
    ]
}
#注意：要想ansible端于远程端的文件保持一致，最好用delete=yes参数
因为，有时候在ansible的目录下删除了某个文件，若不加delete=yes参数的话，远程端的目录下仍然保留有旧的文件！
```



