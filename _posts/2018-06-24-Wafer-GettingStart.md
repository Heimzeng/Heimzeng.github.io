---
layout: post
tags: homework
title: "小程序腾讯云wafer部署"
---
简单几个步骤部署小程序服务器.

# 小程序腾讯云wafer部署
### 通过微信公众平台授权登录腾讯云
打开[微信公众平台](https://mp.weixin.qq.com/)注册并登录小程序，按如下步骤操作：

1. 单击左侧菜单栏中的【设置】。

2. 单击右侧 Tab 栏中的【开发者工具】。

3. 单击【腾讯云】，进入腾讯云工具页面，单击【开通】。

4. 使用小程序绑定的微信扫码即可将小程序授权给腾讯云，开通之后会自动进去腾讯云微信小程序控制台，显示开发环境已开通，此时可以进行后续操作。

### 初始化Demo并上传
1. 打开安装好的微信Web开发者工具([下载链接](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html))点击【小程序项目】。

2. 输入小程序APPID，项目目录选择一个空的目录，接着选择【建立腾讯云Node.js启动模板】，点击确定创建小程序项目。

3. 安装依赖
在刚刚选择的小程序的server目录下安装依赖，如下
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/waferGettingStart/1529830930428.png">
</center>

4. 点击微信开发平台界面的【腾讯云】图标，在下拉的菜单中选择【上传测试代码】
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/waferGettingStart/1529830757488.png">
</center>

5. 上传完代码后，点击详情->腾讯云状态即可看到腾讯云自动分配的开发环境域名
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/waferGettingStart/1529831238435.png">
</center>

6. 完整复制（包括 https://）开发环境 request 域名，然后在编辑器中打开 client/config.js 文件，将复制的域名填入 host 中并保存，保存之后编辑器会自动编译小程序，左边的模拟器窗口即可实时显示出客户端的 Demo：
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/waferGettingStart/1529831701295.png">
</center>

7. 在模拟器中点击【登录】，看到显示“登录成功”，即为开通完成，可以开始其他开发。
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/waferGettingStart/1529831751696.png" width="250px"> <img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/waferGettingStart/1529831812170.png" width="250px"> 
</center>