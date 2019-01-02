## cron模块

```
#注意：cron是为远程主机定义任务计划的
#批量定义远程主机上的定时任务
#首先我们在本地的/etc/ansible/目录下定义一个cron.yml文件

- hosts: 192.168.1.232  #远程主机IP
  remote_user: root    #指定执行的用户
  tasks:                #任务
    - name: cron       #任务名称
      cron: name='cp file' minute=1job='/usr/bin/tmp/script/test.sh'
提示：name 为注释名称，minute为执行任务的时间间隔，job为执行的脚本

#定义好之后，我们执行下ansible-playbook命令
[root@ansibleserver ansible]# ansible-playbook cron.yml
PLAY RECAP********************************************************************
192.168.1.232              :ok=2    changed=1    unreachable=0    failed=0
#出现ok=2 change=1,代表已经在远程机子上做好定时任务了

#在远程主机上查看：
[root@ansible-client script]# crontab -l
#Ansible: cp file
1 * * * * /usr/bin/tmp/script/test.sh
```

```
实例2：
目的：在指定节点上定义一个计划任务，每隔3分钟到主控端更新一次时间
命令：ansible all -m cron -a 'name="custom job" minute=*/3 hour=* day=* month=*weekday=* job="/usr/sbin/ntpdate 172.16.254.139"'
```

```
实例3：
目的：在指定节点上定义一个计划任务，每周一、三、五，每分钟执行
命令：ansible all-m cron -a 'name="custom job" minute=* hour=* day=* month=*weekday=* job="/usr/bin/echo hello"'
```



