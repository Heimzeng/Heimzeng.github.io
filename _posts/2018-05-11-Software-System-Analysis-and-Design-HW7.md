---
layout: post
tags: homework
title: "Software System Analysis and Design HW7"
---
系统分析与设计的第七次作业.

## 美团外卖移动APP订餐业务描述
美团外卖是美团网旗下网上订餐平台，平台上销售外卖品类包括附近美食、水果、蔬菜、超市、鲜花、蛋糕等。而且支持多种支付方式。

以下截图对美团外卖的“订餐“业务作出详细描述。

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/mainpage.png?raw=true" width="200px">

	图1：美团外卖主页面
</center>

图一展示了我们进入美团外卖APP看到的第一个页面，这个页面从上到下分别是：活动、优惠和商家区域。

如果我们想点外卖，首先想到的肯定是点附近商家的外卖，这时候就需要用到定位功能了。点击主界面左上角的位置信息，就可以进入位置设置，如图2所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/location.png?raw=true" width="200px">

	图2：获取定位
</center>

在定位页面中，您可以选择系统自动定位的地址，也可以自己在搜索框中输入地址来设置相应的地点。

设置完地点后，商家信息会更新为附近的商家信息，如图3所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/nearby.png?raw=true" width="200px">

	图3：附近商家
</center>

如果在列表中没有我们想要的商家，我们可以通过搜索功能找到我们想要找的商家，如图4所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/malatang.png?raw=true" width="200px">

	图4：搜索麻辣烫
</center>

如上图所示，我们搜索麻辣烫，会弹出许多的商家，这些商家一般我们定的地点的附近的商家，我们可以按照我们的意愿将他们排序以及进行筛选

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/sort.png?raw=true" width="200px">

	图5：调整搜索顺序
</center>

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/filter.png?raw=true" width="200px">

	图6：筛选
</center>

正如图5和图6所示，我们可以通过排序和筛选轻易得找到我们想要的商家。

在找到目标商家之后，我们就可以进行我们的正式操作——点餐。

我们点击一家商家，就会看到店里出售的许多食品。下拉可以看到商家的详细信息。如图7和图8所示

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/targetStore.png?raw=true" width="200px"> <img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/storeDetail.png?raw=true" width="200px">

	图7：商家主页面 	图8：商家详细信息
</center>

上拉回到餐品选择界面，然后点击每个商品对应的“+“号就可以将它们添加进我们的购物车里。如图9所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/pocket.png?raw=true" width="200px">

	图9：购物车
</center>

这里的购物车跟购物网站上的购物车有所不同，购物网站一般是一个用户对应一个“购物车”，而在美团外卖中，则是每个用户对应每个商家有一个购物车。这就意味着你可以在不同的商家点不同的餐品而不用在更换商家时清空购物车。如下图所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/pocket2.png?raw=true" width="200px">

	图10：另一个购物车
</center>

选完餐品后我们点击去结算，便会跳到一个生成订单的界面，订单有两种类型，如图11和图12所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/order1.jpg?raw=true" width="200px"> <img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/order2.jpg?raw=true" width="200px">

	图11：配送订单 	图12：自取订单
</center>

其中最重要的信息就是用户的地址信息了，假设我们是一个注册并且登录了的用户，我们在第一次订餐的时候肯定要添加一个地址作为配送地址，点击订单中的地址，我们可以进入我们的地址选择界面，里面包括了我们之前添加过的所有地址信息，如果您是一个新用户，地址选择界面便为空。我们可以添加一个地址，如下图所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/addaddr.png?raw=true" width="200px">

	图13：添加地址
</center>

添加完成后这个地址便会出现在我们的地址选择界面的顶部：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/topaddr.jpg?raw=true" width="200px">

	图14：新地址
</center>

我们便可以选择这个地址作为我们的配送地址。

选择完配送地址后如果没有特别的要求，我们就点击提交订单，订单提交后便会跳转到支付页面：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/payorder.png?raw=true" width="200px">

	图15：支付页面
</center>

我们可以使用图中的任何方式支付，支付过程在此不做赘述。

支付完成后便会等待商家接单，商家接单后用户便会进入一个“等待外卖“的过程，餐品的制作以及配送情况都可以在订单界面显示。如果没有在预计送达时间内送达，我们还可以进行催单操作：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/ordering.png?raw=true" width="200px">

	图16：制作配送过程中的订单
</center>

如果外卖送达了，我们会收到一个配送员的电话，在我们收到外卖后，点击图16中的确认收货便可以告知商家我们收到货了，如果很久不点的话，订单会自动跳转到已收货状态。确认后货后这个订单就算是完成了它的生命周期了，如图17所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/ordering.png?raw=true" width="200px">

	图17：订单完成
</center>

但是我们还可以在此订单的基础上对商家进行评价。如图18所示：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/eva.png?raw=true" width="200px">

	图18：评价订单
</center>

至此，一个订餐业务正式结束。

## 美团外卖订餐业务建模

#### 订餐用例图

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/task2usecase.png?raw=true">
</center>

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw7/task2usecase.uxf)

#### 订餐用例活动图

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/task2activity.png?raw=true">
</center>

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw7/task2activity.uxf)

#### 订餐业务领域模型

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/task2model.png?raw=true">
</center>

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw7/task2model.uxf)

#### 订餐业务状态图

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/task2stateModel.png?raw=true">
</center>

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw7/task2stateModel.uxf)

#### 订餐业务顺序图

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw7/task2inorder.png?raw=true">
</center>

[点击下载对应UMLet文件](https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/file/ssaad_hw7/task2inorder.uxf)
