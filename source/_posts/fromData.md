---
title: '''fromData'''
date: 2018-09-03 16:19:13
tags: js
---

## 利用FromData上传文件

htnl

	<form enctype="multipart/form-data" method="post" name="fileinfo" id="upImg">
	            <input type="file" id="uploadBtn" [ngModel]="url" name="uploadFile" (change)="uploadImg($event)" accept="image/png,image/jpeg"/>
	            <!--<button type="submit" id="subBtn">sss</button>-->
	</form>
	
注释：记得将from标签的enctype设置为multipart/form-data，input的name就是上传文件的字段

js 

	var elm = document.getElementById('upImg');
    var forms = new FormData(elm);
    
    forms.append('ObjType', '0100'); //append方法用来添加其他的参数，此例子就是参数名为ObjType，值为'0100';

最后将froms传入post作为data即可；

特殊用法

	formData.append("image", 文件,文件名+".jpg"); //此例子是用来上传base64图片，依次填入的值是，参数名，文件，文件名；
