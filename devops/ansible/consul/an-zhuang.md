#  安装consul

- 下载地址: https://www.consul.io/downloads.html

- 开始安装

```
wget https://releases.hashicorp.com/consul/1.4.0/consul_1.4.0_linux_amd64.zip
 unzip consul_1.4.0_linux_amd64.zip
mv  consul /usr/local/bin/
mkdir -p /etc/consul.d


```

-  /etc/consul.d 添加一个测试的配置文件 node_exporter.json

```
{
  "services":[
 {
  "id": "172.25.31.122_node_exporter",
  "name": "node_exporter",
  "address": "172.25.31.122",
  "port": 9100,
  "tags": ["dev"],
  "checks": [
   {
    "http": "http://172.25.31.122:9100",
    "interval": "5s"
   }
  ]
 },
 {
  "id": "172.25.31.123_node_exporter",
  "name": "node_exporter",
  "address": "172.25.31.123",
  "port": 9100,
  "tags": ["dev"],
  "checks": [
   {
    "http": "http://172.25.31.123:9100",
    "interval": "5s"
   }
  ]
 }
  ]
}
```


- 启动

```
 consul agent -server -ui -bootstrap-expect 1 -data-dir /tmp/consul -config-dir /etc/consul.d -bind=0.0.0.0
```

- nginx代理管理端口

```
upstream consul_upstreams {
                server 127.0.0.1:8500;
}
server {
                listen 8501;
                proxy_pass consul_upstreams;
                #proxy_timeout 1s;
                proxy_connect_timeout 1s;
}

```

-  注册服务

   把上面的json语句用单括号括起来，注册到服务器

```
curl -X PUT -d '{"id": "MySql","name": "MySql","address": "localhost","port": 9104,"tags": ["dev"],"checks": [{"http": "http://localhost:9104/","interval": "5s"}]}'     http://172.25.31.121:8501/v1/agent/service/register

```


- 注销服务
```
curl  --request PUT  http://localhost:8500/v1/agent/service/deregister/MySql
```


- 集群

```
 ./consul agent -server -bootstrap-expect 2 -data-dir=data -node=n1 -bind=10.0.0.5 -client=0.0.0.0 &
 ./consul agent -server -bootstrap-expect 2 -data-dir=data -node=n2 -bind=10.0.0.6 -client=0.0.0.0 &
 ./consul agent -server -bootstrap-expect 2 -data-dir=data -node=n3 -bind=10.0.0.7 -client=0.0.0.0 -ui &
 
 #s1,s2加入s3
 ./consul join 10.0.0.7

 #查询会员
 ./consul members

```

