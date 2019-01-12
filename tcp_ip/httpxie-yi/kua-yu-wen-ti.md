**CORS跨域限制以及预请求验证**

```
'Access-Control-Allow-Origin' : '*'  允许跨域（服务间跨域请求）
'Access-Control-Allow_Headers': 'X-Test-Cors'
'Access-Control-Allow-Methods' : 'POST,PUT,DELETE'
'Access-Control-Max-Age' : '1000'    # 设置验证有效时间
```

**CORS 预请求：**

允许的方法：

1. GET
2. HEAD
3. POST

允许的Content-Type

1. text/plain
2. multipart/form-data
3. application/x-www-form-urlencoded

**缓存头 Cache-Control 的含义和使用（**控制缓存的能力**）**

```
Cache-Control:max-age      // 文档的最大使用期
Expires                    // 文档的绝对的过期日期

```

**缓存验证 Last-Modified 和 Etag 的使用**

```
If-Modified-Since:<date>   // 如果从指定日期之后文档被修改过了，就执行请求的方法
If-None-Match:<tags>       // 为文档提供特殊的标签（参见ETag）
```





