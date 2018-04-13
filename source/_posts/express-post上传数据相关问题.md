---
title: '''express-post上传数据相关问题'''
date: 2018-03-05 18:15:59
tags: express
---


### 在用node服务express的post遇到的问题
**-、上传对象时，express接收到的数据为空**
查看Content-type的设置是否和express的设置一样。

Content-type: application/json 是传输json格式的数据
Content-type: application/x-www-form-urlencoded 是传输from，也可以传输文件，图片；


