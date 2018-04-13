---
title: 用lable自定义radio
date: 2018-03-14 10:47:57
tags: css
---

**lable**
介绍：
label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。如果您在 label 元素内点击文本，就会触发此控件。
就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。
用法：

	<form>
	<label for="male">Male</label>
	<input type="radio" name="sex" id="male" />
	<br />
	<label for="female">Female</label>
	<input type="radio" name="sex" id="female" />
	</form>

label里的for与input的id保持一致就能控制相应的radio。
用lable自定义radio，html部分不变，主要是css部分，要隐藏掉radio；

html部分
<!-- more -->

	<div  class="container">   
	 <form>
	   <input type="radio" id="option-0-1" name="mode" value = "0" class="option-radio" checked />
	   <label for="option-0-1"></label>
	   <span class="">选项一</span>    
	   <input type="radio" id="option-0-2" name="mode" value = "1" class="option-radio" />
	   <label for="option-0-2"></label>
	   <span class="">选项二</span>    
	 </form>
	</div>
	<div  class="container">    disable:    
	  <form>        
	    <input type="radio" id="option-1-0" name="mode" value = "0" class="option-radio" disabled/>
	    <label for="option-1-0"></label>
	    <span class="">选项一</span>        
	    <input type="radio" id="option-1-1" name="mode" value = "1" class="option-radio" disabled/>
	    <label for="option-1-1"></label>
	    <span class="">选项二</span>    
	  </form>
	</div>

css部分

	.option-radio{
	  display: none;
	}
	.option-radio+label{
	  position: relative;
	  height: 20px;
	  width: 20px;
	  border-radius: 50%;
	  border: 1px solid #9a9a9a;
	  background-color: transparent;
	  display: inline-block;
	  top:5px;
	}
	.option-radio:checked+label{
	  position: relative;
	  height: 20px;
	  width: 20px;
	  border-radius: 50%;
	  border: 1px solid rgb(4, 190, 2);
	  background-color: transparent;
	  display: inline-block;
	  top:5px;
	}
	.option-radio:checked+label:after{
	  position: absolute;
	  content: '';
	  font-size: 0;
	  border: 5px solid rgb(4, 190, 2);
	  border-radius: 50%;
	  top:5px;
	  left:5px;
	}
	.option-radio:checked:disabled+label{
	   border-color: #9a9a9a;
	}
	.option-radio:checked:disabled+label:after{
	   border-color: #9a9a9a;
	}
	.option-radio:checked+label:hover,.option-radio + label:hover {
	   cursor: pointer;
	}
	.option-radio:checked+label:active,.option-radio + label:active {
	filter: alpha(opacity=45);
	   -moz-opacity: 0.45;
	   -khtml-opacity: 0.45;
	   opacity: 0.45;
	}
	.container{
	  margin:15px;
	}
	
效果：
![](https://liwuyao.github.io/2018/03/14/用lable自定义radio/radio.jpg)

>把input隐藏，而单选按钮显示的工作全部交由<label>负责。为了使<label>能模拟单选按钮的各种状态，选中、未选中、点击、禁用等状态，这里采用了比较复杂的CSS写法，大量应用了CSS的伪类和伪元素。
例如“.option-radio:checked+label{...}”表示的就是选中状状态下邻近的<label>的显示，此时<label>显示为按钮外面的绿色圆圈边界,而“.option-radio:checked+label:after{...}”表示就是选中状态下<lable>的伪元素after显示为按钮内部的绿色小圆形的显示。依此类推，我们就可以理解未选中、点击和禁用等状态的实现了。
值得注意的一点，上一篇有关CSS的文章中提到的伪元素after，这里也有应用，当然应用的关键点，上一篇中已有介绍，就是position的设置，<label>的css position属性设置为“position: relative;”，而其对应的伪元素after的css position属性设置为“position: absolute;”。圆圈和圆饼的显示都是采用的是设置CSS的border 和border-radius属性。
这里的自定义显示只是简单的使用了CSS的border 和border-radius属性来完成单选按钮圆形外观的显示，比较中规中矩，其实可以根据需要添加其它各种效果，例如加上各种阴影，让按钮更具立体感。或者在不同的状态下启用不同的背景图片，来做出更具个性的按钮。而实现这些所说的效果，主体代码框架会如上面描述那样，不会大的更改，只需改变CSS的某些属性设置就可以做到。

