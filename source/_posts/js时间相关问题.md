---
title: js时间相关问题
date: 2018-07-06 16:45:54
tags: js
---

一、时间戳与日期格式的相互转换

时间戳转日期格式

	function timestampToTime(timestamp) {
	        var date = new Date(timestamp * 1000);//时间戳为10位需*1000，时间戳为13位的话不需乘1000
	        Y = date.getFullYear() + '-';
	        M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
	        D = date.getDate() + ' ';
	        h = date.getHours() + ':';
	        m = date.getMinutes() + ':';
	        s = date.getSeconds();
	        return Y+M+D+h+m+s;
	    }
	    timestampToTime(1403058804);
	    console.log(timestampToTime(1403058804));//2014-06-18 10:33:24

日期转时间戳
<!-- more -->

	var date = new Date('2014-04-23 18:55:49:123');
	    // 有三种方式获取
	    var time1 = date.getTime();
	    var time2 = date.valueOf();
	    var time3 = Date.parse(date);
	    console.log(time1);//1398250549123
	    console.log(time2);//1398250549123
	    console.log(time3);//1398250549000

在实际应用中的小技巧，时间戳转换为yyyy--mm--dd,将转换函数挂载在Data原型上

	Date.prototype.format = function (format) {
	    var o = {
	        "M+": this.getMonth() + 1, //month
	        "d+": this.getDate(), //day
	        "h+": this.getHours(), //hour
	        "m+": this.getMinutes(), //minute
	        "s+": this.getSeconds(), //second
	        "q+": Math.floor((this.getMonth() + 3) / 3), //quarter
	        "S": this.getMilliseconds() //millisecond
	    }
	    if (/(y+)/.test(format)) format = format.replace(RegExp.$1,(this.getFullYear() + "").substr(4 - RegExp.$1.length));
	    for (var k in o) if (new RegExp("(" + k + ")").test(format))format = format.replace(RegExp.$1,RegExp.$1.length == 1 ? o[k] :("00" + o[k]).substr(("" + o[k]).length));
	    return format;
	}

注意：此方式在angular2以上框架不能用，在angular2以上框架可用angular自带的管道进行转换；