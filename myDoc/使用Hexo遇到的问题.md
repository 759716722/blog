---
title: 使用Hexo遇到的问题
date: 2018-03-26 16:51:11
tags:
categories:  
- hexo
---

使用Hexo过程中的问题收集
===
<!-- more -->

1. 如果是代理问题把代理去掉就行了
npm config set proxy null

2. 如果是npm源有问题则使用淘宝npm源
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install hexo-cli -g

3. 如果出现cnpm不是外部命令
因为我之前更改了全局模块安装的路径，因此找不到cnpm的可执行文件，需要配置下环境变量即可
在系统变量 的 PATH下 加入 cnpm.cmd 所在路径
E:\Program Files\nodejs\node_modules\npm\node_global_modules

4. 如果不使用淘宝npm源也能成功下载hexo,但是出现hexo不是外部命令
原因同上更改了全局模块安装的路径
在系统变量 的 PATH下 加入 cnpm.cmd 所在路径
E:\Program Files\nodejs\node_modules\npm\node_global_modules

5. Deployer not found: git
原因是还需要安装一个插件： npm install hexo-deployer-git

6. hexo g 生成的时候报错原因
冒号后面必须有一个空格

7. git下载主题，无法克隆,错误大体描述为“error setting certificate verify locations”
git clone的时候出现一个错误，导致无法克隆成功，错误大体描述为“error setting certificate verify locations”，
翻译为错误设置证书验证位置，看了本地\Git\mingw64\ssl\certs 下面确实有证书。
这个错误是系统证书的问题，系统判断到这个行为会造成不良影响，所以进行了阻止，只要设置跳过SSL证书验证就可以了，
用命令 ： 
    git config --global http.sslVerify false
设置完成后继续clone，就可以了。

8. 在本地server成功，显示没有问题，但是部署到github上之后，就无法显示主题和图片了
更改一下_config.yml文件，其中的url和root属性。
	url: https://759716722.github.io/blog/
	root: /blog
root 下面应该设置成 /你的项目名 而不是/，然后重新部署一下就成功了。

9. 分类栏目不展示分类目录，是因为新建的categories的index.md 未加入 type: "categories" ，导致无法显示分类目录，标签也一样

10. 图片引用出不来
本来以为是因为站点配置文件的post_asset_folder选项没有打开，结果不是因为这个问题，
post_asset_folder设置为true则每新建一遍文章都会新建相应的资源文件夹，所以不采用这种
图片引用采用的是相对路径，因此引用时必须要到相应的目录，通过public目录可以知道
文章的页面目录为：public\2018\04\04\文章名\ 
引用图片为 ： `![小清新](../../../../imgs/loading.gif)`

11. 打开文章的更新时间
搜索 post_meta 将 updated_at 设置为true

12. 打开文章的 字数统计、阅读时间功能
搜索 post_wordcount 将 wordcount、min2read 设置为 true
然后下载 hexo-wordcount 此时我们不进行全局安装，安装在hexo的模块下即可
指令： npm install hexo-wordcount


13. NexT主题自带canvas-nest背景效果不能设置颜色、线条的个数等
可以通过修改_layout.swig，外部引用 canvas-nest.min.js 实现
打开next/layout/_layout.swig 在</body>之前添加代码(注意不要放在< /head>的后面)
 `<script type="text/javascript" color="0,0,255" opacity='0.7' zIndex="-2" count="99" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js"></script>`
color ：线条颜色, 默认: '0,0,0'；三个数字分别为(R,G,B)
opacity: 线条透明度（0~1）, 默认: 0.5
count: 线条的总数量, 默认: 150
zIndex: 背景的z-index属性，css属性用于控制所在层的位置, 默认: -1
注意这里的zIndex只能比-1小，不然会遮住页面所有点击都无法实现




NexT主题配置  http://theme-next.iissnan.com/theme-settings.html


NexT主题优化  https://segmentfault.com/a/1190000013660164

