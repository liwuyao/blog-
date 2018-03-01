---
title: ajax的介绍及使用
date: 2018-02-27 10:31:18
tags: ajax
---

## 介绍

>Ajax 即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。
Ajax = 异步 JavaScript 和 XML（标准通用标记语言的子集）。
Ajax 是一种用于创建快速动态网页的技术。
Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。[1] 
通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
>
### 原生js方法实现ajax
<!-- more -->

>var Ajax={
    get: function(url, fn) {
        var xhr = new XMLHttpRequest();  // XMLHttpRequest对象用于在后台与服务器交换数据          
        xhr.open('GET', url, true);
        xhr.onreadystatechange = function() {
            if (xhr.readyState == 4 && xhr.status == 200 || xhr.status == 304) { // readyState == 4说明请求已完成
                fn.call(this, xhr.responseText);  //从服务器获得数据
            }
        };
        xhr.send();
    },
    post: function (url, data, fn) {         // datat应为'a=a1&b=b1'这种字符串格式，在jq里如果data为对象会自动将对象转成这种字符串格式
        var xhr = new XMLHttpRequest();
        xhr.open("POST", url, true);
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");  // 添加http头，发送信息至服务器时内容编码类型
        xhr.onreadystatechange = function() {
            if (xhr.readyState == 4 && (xhr.status == 200 || xhr.status == 304)) {  // 304未修改
                fn.call(this, xhr.responseText);
            }
        };
        xhr.send(data);
    }
}

注释
一、 open(method, url, async) 方法需要三个参数:
method：发送请求所使用的方法（GET或POST）；与POST相比，GET更简单也更快，并且在大部分情况下都能用；然而，在以下情况中，请使用POST请求：
* 无法使用缓存文件（更新服务器上的文件或数据库）
* 向服务器发送大量数据（POST 没有数据量限制）
* 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠
url：规定服务器端脚本的 URL(该文件可以是任何类型的文件，比如 .txt 和 .xml，或者服务器脚本文件，比如 .asp 和 .php （在传回响应之前，能够在服务器上执行任务）)；
async：规定应当对请求进行异步（true）或同步（false）处理；true是在等待服务器响应时执行其他脚本，当响应就绪后对响应进行处理；false是等待服务器响应再执行。
二、 send() 方法可将请求送往服务器。
三、 onreadystatechange：存有处理服务器响应的函数，每当 readyState 改变时，onreadystatechange 函数就会被执行。
四、 readyState：存有服务器响应的状态信息。
* 请求未初始化（代理被创建，但尚未调用 open() 方法）
* 服务器连接已建立（open方法已经被调用）
* 请求已接收（send方法已经被调用，并且头部和状态已经可获得）
* 请求处理中（下载中，responseText 属性已经包含部分数据）
* 请求已完成，且响应已就绪（下载操作已完成）
五、 responseText：获得字符串形式的响应数据。
六、 setRequestHeader()：POST传数据时，用来添加 HTTP 头，然后send(data)，注意data格式；GET发送信息时直接加参数到url上就可以，比如url?a=a1&b=b1。
### jQuery方法实现ajax

`
$.ajax({
    url: ,
    type: '',
    dataType: '',
    data: {        
    },
    success: function(){    
    },
    error: function(){      
    }
 })
 `
