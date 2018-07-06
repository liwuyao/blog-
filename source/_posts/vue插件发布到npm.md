---
title: '''vue插件发布到npm'''
date: 2018-04-23 14:10:31
tags: 'vue'
---

原理是利用vue提供的插件功能。

### 详细步骤

**一、创建vue插件**

新建一个vue项目，结构目录如下
![](https://liwuyao.github.io/2018/04/23/vue插件发布到npm/img1.png)

	lib里面存放的就是自己写的组件；
	index的内容就是vue插件功能；
	
	import VueComment from './VueComment.vue'
	const comment = {
	  install: function(Vue) {
	    Vue.component(VueComment.name, VueComment)
	  }
	}
	// global 情况下 自动安装
	if (typeof window !== 'undefined' && window.Vue) { 
	    window.Vue.use(comment) 
	}
	// 导出模块
	export default comment

<!-- more -->
**二、修改package.json**

	{
	  "name": "mini-sliders",
	  "description": "vue轮播图组件",
	  "version": "1.0.1",
	  "author": "Echo-lu <echo_lcp@163.com>",
	  // 配置main结点，如果不配置，我们在其他项目中就不用import XX from '包名'来引用了，只能以包名作为起点来指定相对的路径
	  "main":"dist/vue-slider.js",
	  //开源协议
	  "license": "MIT",
	  // 因为组件包是公用的，所以private为false
	  "private": false,
	  "scripts": {
	    "dev": "cross-env NODE_ENV=development webpack-dev-server --open --hot",
	    "build": "cross-env NODE_ENV=production webpack --progress --hide-modules"
	  },
	 // 指定代码所在的仓库地址
	 "repository": {
	 "type": "git",
	 "url": "git+https://github.com/echo-lu/mini-sliders.git"
	 },
	  "dependencies": {
	    "vue": "^2.5.11"
	  },
	  "browserslist": [
	    "> 1%",
	    "last 2 versions",
	    "not ie <= 8"
	  ],
	// 指定关键字
	 "keywords": [
	 "vue",
	 "slider"
	 ],
	  // 项目官网的url
	 "homepage": "https://github.com/echo-lu/mini-sliders/blob/master/README.md",
	  "devDependencies": {
	    ...
	  }
	}

**三、修改webpack.config**

	entry: './src/lib/index.js',
	output: {
	    path: path.resolve(__dirname, './dist'),
	    publicPath: '/dist/',
	    // filename: 'build.js'
	    filename: 'vue-slider.js',
	    library: 'VueSlider',
	    libraryTarget: 'umd',
	    umdNamedDefine: true 

完整的webpack.config:

	var path = require('path')
	var webpack = require('webpack')
	
	module.exports = {
	    // entry: './src/main.js',
	  entry: './src/lib/index.js',
	  output: {
	    path: path.resolve(__dirname, './dist'),
	    publicPath: '/dist/',
	    // filename: 'build.js'
	    filename: 'vue-slider.js',
	    library: 'VueSlider',
	    libraryTarget: 'umd',
	    umdNamedDefine: true 
	  },
	  module: {
	    rules: [
	      {
	        test: /\.css$/,
	        use: [
	          'vue-style-loader',
	          'css-loader'
	        ],
	      },      {
	        test: /\.vue$/,
	        loader: 'vue-loader',
	        options: {
	          loaders: {
	          }
	          // other vue-loader options go here
	        }
	      },
	      {
	        test: /\.js$/,
	        loader: 'babel-loader',
	        exclude: /node_modules/
	      },
	      {
	        test: /\.(png|jpg|gif|svg)$/,
	        loader: 'file-loader',
	        options: {
	          name: '[name].[ext]?[hash]'
	        }
	      }
	    ]
	  },
	  resolve: {
	    alias: {
	      'vue$': 'vue/dist/vue.esm.js'
	    },
	    extensions: ['*', '.js', '.vue', '.json']
	  },
	  devServer: {
	    historyApiFallback: true,
	    noInfo: true,
	    overlay: true
	  },
	  performance: {
	    hints: false
	  },
	  devtool: '#eval-source-map'
	}
	
	if (process.env.NODE_ENV === 'production') {
	  module.exports.devtool = '#source-map'
	  // http://vue-loader.vuejs.org/en/workflow/production.html
	  module.exports.plugins = (module.exports.plugins || []).concat([
	    new webpack.DefinePlugin({
	      'process.env': {
	        NODE_ENV: '"production"'
	      }
	    }),
	    new webpack.optimize.UglifyJsPlugin({
	      sourceMap: true,
	      compress: {
	        warnings: false
	      }
	    }),
	    new webpack.LoaderOptionsPlugin({
	      minimize: true
	    })
	  ])
	}

**四、修改gitignore**
因为要用dist文件夹，所以在.gitignore文件中把dist/去掉。

**五、测试**
首先，打包到本地 
npm run build 
npm pack 
npm pack 之后，就会在当前目录下生成 一个tgz 的文件。 
打开一个新的vue项目，在当前路径下执行(‘路径’ 表示文件所在的位置) 
npm install 路径/组件名称.tgz 
然后，在新项目的入口文件（main.js）中引入

`
import 变量名 from '组件名称'
Vue.use(变量名)
`

**六、发布**
1.在 npm官网 注册一个npm账号
2.切换到需要发包的项目根目录下，npm login登录npm账号，输入用户名、密码、邮箱
3.最后一步，执行npm publish即可

**注意事项**
记得安装cross-env；
它的作用：运行跨平台设置和使用环境变量的脚本；
出现原因：当您使用NODE_ENV =production, 来设置环境变量时，大多数Windows命令提示将会阻塞(报错)。 （异常是Windows上的Bash，它使用本机Bash。）同样，Windows和POSIX命令如何使用环境变量也有区别。 使用POSIX，您可以使用：$ ENV_VAR和使用％ENV_VAR％的Windows。 
说人话：windows不支持NODE_ENV=development的设置方式。会报错
安装命令：npm install --save-dev cross-env；

最好用我写的webpack.config;用vue-cli的改会有问题；期初我用的时候改了半天还是各种问题（可能是我webpack只是入门级的原因，用得6的可以自己去改）；

在组件中用标签引用的时候，就是use里的内容作为标签名；
