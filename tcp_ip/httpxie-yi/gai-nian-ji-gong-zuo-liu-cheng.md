**请求方法：**

1. GET           // 请求某个资源
2. HEAD        // 与get类似，不过只返回状态码
3. PUT           //与读相反，此方法向服务器写入文档
4. POST         // 起初向服务器输入数据
5. TRACE       // 会在目的服务器端发起一个“环回”诊断
6. OPTIONS   // 请服务器删除请求 URL 所指定的资源
7. DELETE     // 请求 Web 服务器告知其支持的各种功能
8. 扩展方法    //方法为开发者提供了一种扩展这些 HTTP 服务能力的手段

**返回状态码：**

| 状态码 | 原因短语 |
| :--- | :---: |
| 1XX | 信息性状态码 |
| 2XX | 成功状态码 |
| 3XX | 重定向状态码 |
| 4XX | 客户端错误码 |
| 5XX | 服务器错误码 |

**URL 与资源：**

* URI ：Uniform Resourc Identifier    统一资源标志符（标识唯一资源）

  * URL : Uniform Resource Locator     统一资源定位符

  * URN ：永久统一资源定位符

URL 通用格式：

```
<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
```

**telnet**模拟**http**请求  localhost 80端口

* GET

```
telnet localhost 80
GET / HTTP/1.1
Host : localhost
```

* POST

```
telnet localhost 80
POST /  HTTP/1.1
Host : localhost
Content-type : application/x-www-form-urlencoded
Content-length : 24
username=hewenshun&age=27
```

**HTTP报文：**

* 请求报文

```
<method> <request-url> <version>    # 起始行 (请求方法 请求路径 所用的协议)
<header>                            # 首部

<entity-body>                       # 主体信息（与首部用一空行分隔）
```

* 响应报文

```
<version> <status> <reason-phrase>   # 起始行
<headers>                            # 首部
<entity-body>                        # 主体
```

请求过程：

```
➜  ~ curl -v http://www.baidu.com
* Rebuilt URL to: http://www.baidu.com/
*   Trying 0.0.0.97...
* TCP_NODELAY set
* Connected to www.baidu.com (127.0.0.1) port 80 (#0)
> GET / HTTP/1.1
> Host: www.baidu.com
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Accept-Ranges: bytes
< Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
< Connection: Keep-Alive
< Content-Length: 2381
< Content-Type: text/html
< Date: Fri, 11 Jan 2019 16:40:25 GMT
< Etag: "588604eb-94d"
< Last-Modified: Mon, 23 Jan 2017 13:28:11 GMT
< Pragma: no-cache
< Server: bfe/1.0.8.18
< Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/
< 
<!DOCTYPE html>
...
```



