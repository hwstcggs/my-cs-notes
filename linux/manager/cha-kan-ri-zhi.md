**cat ：显示文件所有内容**

```
显示文件所有内容：cat filename
显示文件内容的时候，添加行号：cat -n filename
将2个文件合并为1个文件：cat file1 file2 > file3
将文件file1中的内容拷贝到file2中：cat file1 > file2
创建一个新文件：cat > file
```



**less：分页加载文件，可以上下翻页**

```
less filename （在查看之前不会加载整个文件）
按空格键，向文件尾部滚动一页
按回车键，向文件尾部滚动一行
​
按b,向文件头部滚动一页
按y,向文件头部滚动一行
​
也可以用鼠标上下滚动翻页
​
输入/xxxx或者?xxxx，可以在文档中搜索字符串xxxx
​
加入-N参数，可以显示行号（大写的N，小写的n无效）
​
输入:G跳到文件尾部
```



**more**

```
从第100行开始显示文件内容，每页显示50行：more -50 +100 filename
​
加入-N参数，可以显示行号（大写的N，小写的n无效）
```



**tail ：显示文件后n行内容**

```
显示文件最后10行内容：tail -n 10 filename 
如果filename中的内容正在改变，加上-f会不断刷新，可以看到最新的文件内容：tail -f filename 
查看最后10行，并不断刷新：tail -fn 10 filename
```



**head：显示文件前n行内容**

```
显示文件前10行内容：head -n 10 filename
```



**清空文件内容**

```
# 方式①
$ :> filenname
​
# 方式②
$ > filename
​
# 方式③
$ echo "" > filename
​
# 方式④
$ echo > filename
​
# 方式⑤
$ cat /dev/null > filename
​
# 方式⑥
$ echo /dev/null > filename
​
# 方式⑦
$ cp /dev/null > filename
```



