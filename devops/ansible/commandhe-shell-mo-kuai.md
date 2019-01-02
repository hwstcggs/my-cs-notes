#  command 模块和shell

用于在各被管理节点运行指定的命令

shell和command的区别：shell模块可以特殊字符，而command是不支持

* #### command模块 {#1command模块}

– chdir：在运行命令之前，切换到此目录

```
- name: return motd to registered var
  command: cat /etc/motd
  register: mymotd

- name: Run the command if the specified file does not exist.
  command: /usr/bin/make_database.sh arg1 arg2 creates=/path/to/database

# 您还可以使用“args”表单提供选项。
- name: This command will change the working directory to somedir/ and will only run when /path/to/database doesn't exist.
  command: /usr/bin/make_database.sh arg1 arg2
  args:
    chdir: somedir/
    creates: /path/to/database
```

* #### shell模块 {#2shell模块}

– chdir：在运行命令之前，切换到此目录

– executable：更改用于执行命令的shell（bash，sh）。 应该是可执行文件的绝对路径

```
- name: Execute the command in remote shell; stdout goes to the specified file on the remote.
  shell: somescript.sh >> somelog.txt

- name: Run a command that uses non-posix shell-isms (in this example /bin/sh doesn't handle redirection and wildcards together but bash does)
  shell: cat < /tmp/*txt
  args:
    executable: /bin/bash
```



