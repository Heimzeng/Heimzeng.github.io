---
layout: post
tags: homework
title: "Software System Analysis and Design HW6"
---
系统分析与设计的第六次作业.

## 参考[Asg_RH文档](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw6/Asg_RH.pdf)，对Reservation/Order对象进行状态建模

分析可知，订单对象的
- 状态集合$S = {待确认, 已确认, 已支付, 已完成, 退款中, 已取消}$
- 事件集合$E = {创建订单, 确认订单, 支付订单, 取消订单, 入住, 超时, 退款}$

根据以上状态集合和事件集合我们得到以下的状态模型

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw6/stateModel.png?raw=true)

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw6/stateModel.uxf)

## 对淘宝退货业务对象状态建模

分析可知，淘宝退货业务对象的
- 状态集合$S = {待发货, 已发货, 已签收, 退货处理中, 物流召回中, 等待买家寄回, 待退款, 已退款, 退货完成}$
- 事件集合$E = {订单支付成功, 确认订单, 买家收货, 退货, 商家同意退货, 商家不同意退货, 退款, 物流召回, 买家寄回超时...}$

根据以上状态集合和事件集合我们得到以下的状态模型

![](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw6/stateModel2.png?raw=true)

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw6/stateModel2.uxf)
