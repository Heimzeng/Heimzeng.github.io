---
layout: post
tags: homework
title: "微信web开发者工具入门"
---
微信web开发者工具是我们用来开发小程序的平台，也是我们必须学习的一个很好的工具.

## 安装
下载地址：！[微信web开发者工具下载](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html?t=2018412)
## 使用
安装完成后打开，使用关联了小程序账号的微信进行扫码登录
！[](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/login.jpg)
登录完成后进入到项目选择界面，由于我们开发的是小程序，所以选择新建小程序
![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/mainpage.png)
进入小程序创建页面，我们需要新建一个空目录给我们的小程序，并且填入对应的APPID，再输入我们的项目名称
![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/createAProject.png)
当然你也选择无APPID的体验模式，但是小程序的部分功能会受到限制
![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/createAProject_noID.png)
点击确定我们就可以得到一个初始的小程序了
![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/helloworld.png)

接下来我们学习如何使用微信web开发者工具
主界面分为左中右三块，左边是当前小程序的实时展示和操作，中间部分是整个Project的目录，右边部分是编码部分
在pages整个目录下，一个子目录代表一个页面，里面装的只能是以页名开头的不同后缀名的文件
比如index页面目录下，就只有index.\*这样的文件
通过我们之前学到的web相关知识来看，小程序的网页都由js脚本动态生成。于是我们可以尝试修改一些数据，比如，把初始的Hello World改成我们的项目名"布鲁电影"
点击编译便可以看到更改后的效果
![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw3/changeTitle.png)

至此，我们搭建了小程序开发的基本环境，并了解了该工具的基本布局和操作，在设计工作完全完成后，我们会开始进一步的编码工作。