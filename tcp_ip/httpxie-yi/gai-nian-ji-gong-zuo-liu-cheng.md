* [ ] **telnet**模拟**http**请求  localhost 80端口

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
Content-length : 24
username=hewenshun&age=27
```

**HTTP报文：**

* 请求报文

```
<method> <request-url> <version>
<header>
<entity-body>
```

* 响应报文

```
<version> <status> <reason-phrase>
<headers>
<entity-body>
```

**请求方法：**

1. GET     // 请求某个资源
2. HEAD    // 与get类似，不过只返回状态码
3. PUT      //与读相反，此方法向服务器写入文档
4. POST    // 起初向服务器输入数据
5. TRACE   // 会在目的服务器端发起一个“环回”诊断
6. OPTIONS   // 请服务器删除请求 URL 所指定的资源
7. DELETE   // 请求 Web 服务器告知其支持的各种功能
8. 扩展方法  / /方法为开发者提供了一种扩展这些 HTTP 服务能力的手段

**返回状态码：**

| 状态码 | 原因短语 |
| :--- | :--- |
| 1XX | 信息性状态码 |
| 2XX | 成功状态码 |
| 3XX | 重定向状态码 |
| 4XX | 客户端错误码 |
| 5XX | 服务器错误码 |





