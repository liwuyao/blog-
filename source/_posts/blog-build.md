---
title: 用hexo和github搭建博客
date: 2018-02-26 14:43:46
tags: blog
---

## 详细步骤

 一、github
去申请一个github账户，注意最好有英文格式的游戏，而不是像qq号加@那种。
Git需要配置ssh钥匙

git的操作步骤，步骤如下：

在git（需要安装，百度一下就知道），输入git config --global user.name "superGG1990"，用来设置自己的get用户名，
superGG1990就是你自己的名字（记得更改），

在git输入git config --global user.email "superGG1990@163.com"，用来关联你的邮箱，这个邮箱就是注册的github的邮箱，
 然后去找到生成ssh钥密的文件，一般在c/user/.ssh/,文件名叫id_dsa.pub，复制里面的钥密（全部复制），在github上配置。（具体一些细则请百度）；

登陆之后，点击页面右上角的加号，选择New repository：

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository.jpg)	

<!-- more -->

新建代码库：
进入代码库创建页面
在Repository name下填写yourname.github.io，Description (optional)下填写一些简单的描述（不写也没有关系），如图所示：

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository2.jpg)	

**注意：比如我的github名称是李伍尧 ,这里你就填 gdutxiaoxu.github.io,如果你的名字是xujun，那你就填 xujun.github.io**

代码库的设置：

接下来开启gh-pages功能，进入刚才创建的库，点击界面右侧的Settings，你将会打开这个库的setting页面，向下拖动，直到看见GitHub Pages，如图：

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository3.jpg)

Github pages

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository4.jpg)

点击Automatic page generator，Github将会自动替你创建出一个gh-pages的页面。 如果你的配置没有问题，那么大约15分钟之后，yourname.github.io这个网址就可以正常访问了~ 如果yourname.github.io已经可以正常访问了，那么Github一侧的配置已经全部结束了。

到此搭建hexo博客的相关环境配置已经完成，下面开始讲解Hexo的相关配置

二、hexo

[hexo文档地址](https://hexo.io/zh-cn/docs/)
按照官方文档安装好hexo

安装好后，接下来是对hexo的相关配置

在_config.yml进行如下配置：

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository7.png)

在cdm的输入
`hexo init`	
此命令是用来生成静态文件
然后输入
`hexo s`
此命令是启动服务

在浏览器中打开http://localhost:4000/，你将会看到：

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository5.jpg)

这是在本地浏览是否成功。

如果你想换个主题（主题指整个网站的样式，布局）,先去网上找好别人做的的主题，我用的是yilia这个主题，下好主题后，将主题放入themes,
然后在博客的根目录下的_config.yml文件中找到theme，将参数改成你所找的主题，如图：

![](https://liwuyao.github.io/2018/02/26/blog-build/new_repository6.png)

安装hexo-deployer-git自动部署发布工具
`npm instal lhexo-deployer-git  --save`
最后发布到hexo clean && hexo g && hexo d

**补充hexo的命令**

新建文章
`hexo new "name"`
如hexo new "hello-world“
执行此命令后会在根目录下创建一个name.md的文件。次文件就是用来写博客的。在写博客之前得知道些markdown的语法。

新建文件夹
`hexo new page "photo"`
执行此命令后会在根目录的source生成文件夹。在生成静态文件后，文件夹的位置会变到根目录下（public文件夹里存放的是静态文件）

其他hexo的相关操作，请参考hexo的官方文档。