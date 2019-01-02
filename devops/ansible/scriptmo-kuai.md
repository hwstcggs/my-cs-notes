## script模块 {#script模块}

在远程主机上执行脚本

```
[root@Ansible ~]# chmod +x /tmp/script.sh 
[root@Ansible ~]# cat /tmp/script.sh 
#!/bin/bash
echo 'This is a test script' > /tmp/script.ansible
useradd Jack_wang
[root@Ansible ~]#
```

```
[root@Ansible ~]# ansible test_hosts -m script -a '/tmp/script.sh'
Enter passphrase for key '/root/.ssh/id_rsa': 
192.168.31.110 | SUCCESS => {
    "changed": true, 
    "rc": 0, 
    "stderr": "Shared connection to 192.168.31.110 closed.\r\n", 
    "stdout": "", 
    "stdout_lines": []
}
[root@Ansible ~]# ansible test_hosts -a "id Jack_wang"
192.168.31.110 | SUCCESS | rc=0 >>
uid=502(Jack_wang) gid=502(Jack_wang) groups=502(Jack_wang)
[root@Ansible ~]# ansible test_hosts -a "cat /tmp/script.ansible"
192.168.31.110 | SUCCESS | rc=0 >>
This is a test script
[root@Ansible ~]#
```



