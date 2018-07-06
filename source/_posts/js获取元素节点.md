---
title: js获取元素节点
date: 2018-07-06 17:16:07
tags:js
---

	<div id="dom"></div>
	 function dom(){
	   var a = document.getElementByIdx_x_x("dom");
	   var b = a.childNodes;   获取a的全部子节点
	   var c = a.parentNode;   获取a的父节点
	   var d = a.nextSbiling;   获取a的下一个兄弟节点
	   var e = a.previousSbiling;获取a的上一个兄弟节点
	   var f = a.firstChild;    获取a的第一个子节点
	   var g = a.lastChild;     获取a的最后一个子节点
	}