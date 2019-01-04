---
title: react-native使用总结
date: 2019-01-04 14:24:54
tags:
---

**一、版本问题**
  现在的android的开发都要求开发8.0以上的版本。在开发前就得用andorid-studio升级到8.0的sdk；

**二、react-native-video插件的使用问题**
 该插件存在一些android兼容问题。如果遇到是因为你的jar包是基于jdk 1.8的，但当前AS（2.3.1）默认使用的jdk是1.7的；
 在app/build.gradle的android对象里加入
 	
	 compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
**三、react-native-swiper插件的问题**
该插件在使用scrollBy时候经常出现无反应的问题，等一系列其他问题。当轮播可以，但是不能用作滑动切换工具用，如果要作为切换工具使用
更改使用teaset这个UI库里的swiper，这个库的问题较少，不需花太多精力去适配。

**四、使用iconfont**
1.首先在将选好的iconfont下载到本地，将iconfont.ttf文件放入android/app/src/main/assets/fonts文件夹里;
2.安装react-native-vector-icons安装步骤网上搜索一打把;
3.创建一个转译iconfont的js文件，此处我命名为oneIconFont,内容如下：
	
	import {createIconSet} from 'react-native-vector-icons'

	const glyphMap = {//此处key值是自定义图标的名称，值是，iconfont的Unicode转换成的10进制，就是16进制换行为10进制；
	  icongedan: 58986,
	  music:59008,
	  play:59240,
	  list:58965,
	  search:59004,
	  stop:58962,
	  play2:58901,
	  xiala:58971
	}
	
	const OIcon = createIconSet(glyphMap, 'iconfont', 'iconfont.ttf')
	
	export {OIcon}

	
4.创建一个icon组件，内容如下：

	import FontAwesome from 'react-native-vector-icons/FontAwesome'
	import {OIcon} from './oneIconFont'
	import React, {Component} from 'react'
	import PropTypes from 'prop-types'
	
	const iconMap = {
	  fontAwesome: FontAwesome,
	  oneIcon: OIcon
	}
	
	class Icon extends Component {
	
	  render() {
	    const {name, size, color} = this.props
	    if (!name.includes('|')) {
	      throw new Error('name 解析错误！')
	      return null
	    }
	    let nameArr = name.split('|')
	    let fontlib = nameArr[0]
	    let font = nameArr[1]
	    let CustomIcon = iconMap[fontlib]
	    if (!CustomIcon) throw new Error('没有找到匹配的font库，请review代码！')
	    return (
	      <CustomIcon name={font} size={size} color={color}/>
	    )
	  }
	}
	
	Icon.propTypes = {
	  name: PropTypes.string.isRequired,
	  size: PropTypes.number.isRequired,
	  color: PropTypes.string.isRequired
	}
	
	export {Icon}

5.使用：
	
	import {Icon} from './component/icon'
	
	<Icon name={'oneIcon|xiala'} size={25} color={'white'}/>
	
**五、动画和事件同时执行卡顿问题**

	InteractionManager.runAfterInteractions(() => {
	    this.setState({
	  		isShowSongList:true
	  	})
	});
使用此方法解决，此方法的意思是在动画执行完成后在执行事件。

**六、render()渲染问题**
	
每次用数据改变视图都会调用一次render()函数，所以render函数的调用不能频率过高，会造成动画的阻塞。在改变视图的同时，动画也在执行，就会
看见动画有卡顿问题。而且视图的改变频率不能超过250ms一次；
