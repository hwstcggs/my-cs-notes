telnet模拟http请求  localhost 80端口

* GET

```
telnet localhost 80
GET / HTTP/1.1
Host : localhost
```

* POST

```
telnet localhost 80
POST / HTTP/1.1
Host : localhost
Content-type : application/x-www-form-urlencoded
Content-length : 23
username=hewenshun&age=27
```



