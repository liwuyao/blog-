---
title: vue-can-hide-select
date: 2018-07-05 16:52:09
tags: vue
---

此插件是超行可省略插件，只应用于vue，此插件优点除了可以超行省略，还有就是样式可以最大自由化，是以直接填写style来控制
效果图如下

![](https://liwuyao.github.io/2018/07/05/vue-can-hide-select/vue-can-hide-demo.png)

git地址：https://github.com/liwuyao/can-hide-select；
安装：npm install can-hide-select
使用说明：
main.js中引用

	import hideSelect from 'can-hide-selcet'
	Vue.use(hideSelect);
	
在组件中引用

	<can-hide-select :data="options" :config="selectConfig" v-if="open" v-on:selectVal="selectRes"></can-hide-select>

data的类型：1、[‘测试1’，‘测试2’]，2、[{value:1,lable:'测试1'}，{value:2,lable:'测试2'}]；
config是填写相关配置，具体说明如下

	isLable:false, //如果data是1类型,可以不填，如果data是2类型，值设置成true
	optionCalssName:'', //可以设置自己设定的class名给option
	selectVal:'请输入', //select的值，可以用来初始化设置（目前版本只能默认首选为第一个）
	selectStyle:'',  //最外框的样式
	valueStyle:'',  //select框的style
	optionStyle:'', //option的style
	iconStyle:'',  //下拉icon的style
	optionBoxStyle:'', //option外框的style
	optionOutBoxStyle:'', //option最外框的style
	
selecVal是返回值函数，在组建中用一个函数接收

	methods:{
	  	selectRes(val){
	  		console.log(val);
	  	}
	}
