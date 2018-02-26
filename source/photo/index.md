---
title: 相册
noDate: 'true'
---

<link rel="stylesheet" href="../css/photo.css" />
<div style="overflow:hidden;" id="ph-box">
</div>
<script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
<script src="../js/test.js"></script>
<script>
		var phData=[
			{
				jsonData:"2018_2_24.json",
				elm:"ph-2018_2_24",
				day:"2018.2.25",
				adress:"2018_2_24"
			},
			{
				jsonData:"2018_2_26.json",
				elm:"ph-2018_2_26",
				day:"2018.2.26",
				adress:"2018_2_26"
			}
		]
			function creat(data,elm,more,day,adress){
				var boxElm = document.createElement("div");
					boxElm.id=elm;
					boxElm.style="overflow:hidden;position: relative;padding-bottom:40px;";
					document.getElementById("ph-box").appendChild(boxElm);
			    var moreElm=document.createElement("div");
			    	moreElm.style="line-height:30px;height:30px;position:absolute;bottom:0;width:100%;color:red;text-align:right;cursor:default;"
			    	moreElm.innerHTML="MORE";
			    	moreElm.onclick=()=>{
			    		getMore(data,elm,true,day,adress);
			    	}
				$.get(data,function(data){
				var box = document.getElementById(elm);
					box.innerHTML="";
				var father =box.parentNode
				var html = "";
				var num = data.length;
					if(data.length >= 12){
						num = 12;
					}
					if(more){
					 num=data.length;
					}
				for(let i=0;i<num;i++){
					var demo = '<img src="'+'../gallery/'+adress+'/'+data[i]+'" />';
					html += demo;
				}
				var date = '<h3>'+day+'</h3>';
				box.innerHTML=date+html;
				if(data.length > 12 && !more){
						box.appendChild(moreElm);
					}
				})
			}
			for(let j = 0;j<phData.length;j++){
				creat(phData[j].jsonData,phData[j].elm,null,phData[j].day,phData[j].adress);
			}
			function getMore(data,elm,more,day,adress){
				creat(data,elm,more,day,adress);
			}
</script>

