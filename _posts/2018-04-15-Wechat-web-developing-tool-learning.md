---
layout: post
tags: homework
title: "微信web开发者工具入门"
---
微信web开发者工具是我们用来开发小程序的平台，也是我们必须学习的一个很好的工具.

## 安装
下载地址：[微信web开发者工具下载](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html?t=2018412)

## 新建项目
安装完成后打开，使用关联了小程序账号的微信进行扫码登录。

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/login.jpg?raw=true)

登录完成后进入到项目选择界面，由于我们开发的是小程序，所以选择新建小程序。

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/mainpage.png?raw=true)

进入小程序创建页面。我们需要新建一个空目录给我们的小程序，并且填入对应的APPID，再输入我们的项目名称。

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/createAProject.png?raw=true)

当然你也选择无APPID的体验模式，但是小程序的部分功能会受到限制。

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/createAProject_noID.png?raw=true)

点击确定我们就可以得到一个初始的小程序了。

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/helloworld.png?raw=true)

接下来我们学习如何使用微信web开发者工具。

主界面分为左中右三块，左边是当前小程序的实时展示和操作，中间部分是整个Project的目录，右边部分是编码部分。

在pages整个目录下，一个子目录代表一个页面，里面装的只能是以页名开头的不同后缀名的文件。

比如index页面目录下，就只有index.\*这样的文件。

通过我们之前学到的web相关知识来看，小程序的网页都由js脚本动态生成。于是我们可以尝试修改一些数据，比如，把初始的Hello World改成我们的项目名"布鲁电影"。

点击编译便可以看到更改后的效果。

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/changeTitle.png?raw=true)

至此，我们搭建了小程序开发的基本环境，并了解了该工具的基本布局和操作，在设计工作完全完成后，我们会开始进一步的编码工作。

## 先修知识
在开始小程序开发之前，还是得有一定的web开发基础。包括但不限于：HTML、CSS、JavaScript、xml、json等。

[w3cschool](http://www.w3school.com.cn/)是学习web方面知识的一个很好的网站，本人在学习web开发前期也是通过该网站入门的。

## 从零开始
在开始编码前我们首先得熟悉下小程序的各种文件格式，总共四种如下

|文件类型|作用|
|---|---|
|\*.js|JavaScrip文件|
|\*.json|项目配置文件，负责窗口颜色等等|
|\*.wxml|类似HTML文件|
|\*.wxss|类似CSS文件|

一个初始小程序根目录下一般会包括以下的文件/文件夹

|文件名/文件夹|作用|
|---|---|
|app.json|整个小程序的基本配置文件|
|app.js|全局脚本文件，也是整个小程序的入口|
|app.wxss|一个非必须的文件，类似于全局css文件|
|project.config.json|项目配置文件|
|./pages|页面的目录，每个目录代表一个页面|
|./logs|后台日志组件的目录|

了解了这些文件以及对应的用处之后，相信学习过web开发的同学都已经知道对应文件的作用以及应该如何在对应的文件里编码了。

接下来就等待设计文档的完成，然后就可以开始对应的编码环节了。