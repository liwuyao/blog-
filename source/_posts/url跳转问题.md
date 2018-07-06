---
title: url跳转问题
date: 2018-07-06 16:18:20
tags: url跳转
---

在一些业务中，我们需要做打开新网页的操作，但是goole浏览器会因为安全问题拦截这样的操作，需要人为去取消这样的拦截。如果让用户自己去取消拦截，这样会导致体验很差，且大多数用户不知道如何取消拦截

解决方案1

如果是跳转已有页面不做业务上的操作，设置a标签的target为"_blank"
<a href="" target="_blank"></a>

解决方案2

如果想要在跳转前做普通操作

	window.open(url)

解决方案3	
如果在跳转前想要做提交表单请求，浏览器会拦截，解决方法如下。
	
	var win = window.open(url) //win就相当于新窗口，你可以做win.body,win.document.getElementById等操作。url也可是静态html路径；
		win.document.forms[0].submit()
	

