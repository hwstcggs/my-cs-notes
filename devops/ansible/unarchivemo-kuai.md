### unarchive模块 {#14unarchive模块}

用于解压文件，模块包含如下选项： 

– copy：在解压文件之前，是否先将文件复制到远程主机，默认为yes。若为no，则要求目标主机上压缩包必须存在。 

– creates：指定一个文件名，当该文件存在时，则解压指令不执行 

– dest：远程主机上的一个路径，即文件解压的绝对路径。 

– group：解压后的目录或文件的属组 

– list\_files：如果为yes，则会列出压缩包里的文件，默认为no，2.0版本新增的选项 

– mode：解压后文件的权限 

– src：如果copy为yes，则需要指定压缩文件的源路径 

– owner：解压后文件或目录的属主



```
- name: 将foo.tgz解压缩到/var/lib/foo中
  unarchive:
    src: foo.tgz
    dest: /var/lib/foo

- name: 解压远程计算机上已存在的文件
  unarchive:
    src: /tmp/foo.zip
    dest: /usr/local/bin
    remote_src: yes

- name: 解压文档需要下载的文件（2.0中添加）
  unarchive:
    src: https://example.com/example.zip
    dest: /usr/local/bin
    remote_src: yes
```



