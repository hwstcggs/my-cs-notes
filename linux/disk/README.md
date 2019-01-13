找出占用空间最大的文件

```
$ cd/path/to/some/where
$ du -hsx * | sort -rh | head -10
//命令解释
du : 计算出单个文件或者文件夹的磁盘空间占用.
sort : 对文件行或者标准输出行记录排序后输出.
head : 输出文件内容的前面部分.
```



