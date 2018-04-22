---
layout: post
tags: homework
title: "Software System Analysis and Design HW4"
---
系统分析与设计的第四次作业.

## 1. 用例建模
**a. 阅读 Asg_RH 文档，按照Task1要求绘制用例图。**

[Asg_RH](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw4/Asg_RH.pdf)

绘制用例图如下：

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw4/task1usecase.png?raw=true)

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw4/task1usecase.uxf)

**b. 选择你熟悉的定旅馆在线服务系统（或移动 APP），如绘制用例图。并满足以下要求：**
- 对比 Asg_RH 用例图，请用色彩标注出创新用例或子用例
- 尽可能识别外部系统，并用色彩标注新的外部系统和服务

个人选择了美团的旅馆系统，绘制用例图如下：

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw4/meituanHotel.png?raw=true)

其中背景为蓝色的组件为新增的服务或子用例

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw4/meituanHotel.uxf)

**c. 对比两个时代、不同地区产品的用例图，总结在项目早期，发现创新的思路与方法**

我们知道，a中的用例图是国外的早期的酒店预订系统，b中是当前国内流行的酒店预订系统。

通过分析我们得到一些总结：
- 在项目的早期，我们可以参考过往项目的用例图，提取核心用例作为自己的核心用例，这样子可以快速构造出一个可用的系统
- 在创新上，我们可以在以往的基础上进行改进，加入一些自动化的元素或者本土化的元素，比如b中的获取定位和使用优惠券

**d. 请使用 SCRUM 方法，在（任务b）用例图基础上，编制某定旅馆开发的需求（backlog）**

backlog如下：

|ID|NAME|IMP|EST(week)|NOTE|
|---|---|---|---|---|
|1|微信登录|50|1|接入微信API|
|2|查找酒店|40|5|接入酒店信息，提供排序、筛选等功能|
|3|预订酒店|50|10|接入酒店系统，提供详细酒店信息|
|4|管理订单|50|8|接入微信支付、银联支付系统|
|5|优惠券系统|20|2|优惠券的获取和使用|

## 2. 业务建模
**a. 在（任务b）基础上，用活动图建模找酒店用例。简述利用流程图发现子用例的方法**

活动图如下：

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw4/meituanHotelActivity.png?raw=true)

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw4/meituanHotelActivity.uxf)

利用流程图，可以把一个用例的业务流程清晰地展现出来，从中寻找可以抽象、复用的部分，并把它们抽象为子用例。

**b. 选择你身边的银行 ATM，用活动图描绘取款业务流程**

活动图如下：

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw4/bankActivity.png?raw=true)

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw4/bankActivity.uxf)

**c. 查找淘宝退货业务官方文档，使用多泳道图，表达客户、淘宝网、淘宝商家服务系统、商家等用户和系统协同完成退货业务的过程。分析客户要完成退货业务，在淘宝网上需要实现哪些系统用例**

退货业务的多泳道图如下：

## 用例文本建模
三种用例文本分别是：摘要、非正式和详述。

- 摘要：简洁的一段式摘要，通常用于主成功场景。
	- 优点：语言简洁，在早期需求分析中，能够快速了解主题和范围，是一种比较高效的用例文本编写模型。
	- 缺点：场景描述不够详尽，不利于给出开发过程中的细节。
- 非正式：非正式的段落格式，用几个段落覆盖不同场景。
	- 优点：同样比较简短，不需要花费大量的时间进行编写，比摘要要多一些场景，能够清楚一点地了解到各种场景的情况。
	- 缺点：仍然是不够详尽，对于开发来说不足以提供足够的信息，还需要进一步的精细。
- 详述：详细编写所有步骤及各种变化，同时具有补充部分，如前置条件和成功保证。
	- 优点：非常详尽，考虑到所有的情况与场景，能够给开发提供有力的帮助。
	- 缺点：编写详述用例需要花费很多时间，过程繁琐。