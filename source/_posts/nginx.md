---
title: nginx 简单用法
date: 2018-03-13 17:06:30
tags: serve
---

### 介绍

Nginx (engine x) 是一个高性能的HTTP和反向代理服务器

**常用命令**
start nginx : 启动nginx
nginx -s reload  ：修改配置后重新加载生效
nginx -s reopen  ：重新打开日志文件
nginx -t -c /path/to/nginx.conf 测试nginx配置文件是否正确

关闭nginx：
nginx -s stop  :快速停止nginx
nginx -s quit  ：完整有序的停止nginx


如果遇到报错：
bash: nginx: command not found

有可能是你再linux命令行环境下运行了windows命令，

如果你之前是允许 nginx -s reload报错， 试下 ./nginx -s reload

或者 用windows系统自带命令行工具运行
<!-- more -->
**配置**

nginx配置文件在 nginx-1.8.0\conf\nginx.conf

`
http {
     gzip  on;

    #一个server就是一个服务
    server {
        listen       80;#监控的端口;
        server_name  static.cnblog.com;#监听端口的域名如http://192.168.201.27，一般就是localhost;
		#静态文件
        location / {
            root   G:/source/static_cnblog_com;
        }
        #html文件
        location / {
            root   G:/source/html/mobile/dist;
            index  index.html index.htm;
        }
        location /request {
            root /;
            proxy_set_header  Host $host; #请求主机头字段，否则为服务器名称。
            proxy_headers_hash_max_size 1024; #存放http报文头的哈希表容量上限,默认为512个字符
            proxy_headers_hash_bucket_size 128; #设置头部哈希表大小 默认为64
            proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for ;
            proxy_set_header Accept-Encoding "";
            proxy_pass http://localhost:8888/login/; #请求替换地址 例如要请求http://localhost:8888/login/ 也就是请求http://localhost/request/
        }
    }
}
`

location/表示访问的路径是localhost， location /request，表示访问的是localhost /request；