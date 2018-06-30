---
layout: post
tags: homework
title: "布鲁电影报告"
---
分为后台开发方面和团队管理方面.

# 后台开发
## 熟悉ES6
在搭建了wafer框架之后，首先要做的并不是看wafer的档案，也不是看源码，而是需要熟悉最基础的，也就是小程序和wafer的共同开发语言：JS

虽然本人之前对ES有过一段时间的接触，但是由于时间久远而且不够深入，所以现在忘得差不多了

主要看的是[阮一峰老师的博客](http://es6.ruanyifeng.com/#README)，全面而且易懂，让我尽可能快地入门了ES6，也了解了跟以往的一些不同，最大的感慨就是，好像很多语言都在像python的语法靠拢，尽量地减轻程序员的门槛和工作量，也是一个不错的趋势啊

## 熟悉wafer
阮一峰老师的ES6教程已经完全足以用于开发一个中型的小程序了，于是我开始熟悉wafer这个框架。

这是一个腾讯云团队开发的用于【快速构建具备弹性伸缩能力的微信小程序】的框架，本项目（BruMovie）用的是wafer的最新版[wafer2](https://github.com/tencentyun/wafer)，其中集成了小程序wx模块、koa框架以及knex.js，几乎涵盖所有的开发场景。

由于不管是wx模块、koa框架还是knex.js本人都是第一次接触，所以每一个都需要去看一下入门文档，其实查文档的时间都快赶上真正的开发时间了。

## 开发环节
在充分熟悉了开发语言和使用框架之后，我们就开始开发我们的小程序了
### 数据库
小程序的所有操作其实基本都可以看成是客户端和服务器交换数据的过程，所以数据库是一个至关重要的东西，于是本人开始根据领域模型设计数据库。由于初期的领域模型也不是特别的完美，所以在设计的时候会根据实际需要来设计实体表以及关系表。领域模型如下：
![](https://github.com/BruMovie/Dashboard/blob/gh-pages/doc/DomainModelDiagram/domainmodel.png?raw=true)

根据领域模型我们设计了刚好20个表格，他们的名字和表项分别如下：

### 登录
打开一个小程序，首先我们要做的就是登录环节了，其实wafer已经给了我们内置好了一个登录模块，不过由于小程序的官方API更新的比较快，demo中有些接口也是过时的，所以我们在原来的基础上加以改进，使得我们有了一个与时俱进的登录接口，微信的登录流程如下：
- 用户使用```wx.login()```获取code传给开发者服务器
- 开发者服务器以code换取 用户唯一标识openid 和 会话密钥session_key
- 服务器返回数据，并将userInfo储存在数据库中备用

然后服务器就可以使用这两个东西进行登录、用户验证以及会话的管理

### 验证
在登录之后，当用户每次获取或者提交敏感数据的时候（本程序中这种情况为：使用post请求的时候），用户需要向服务器传递自己的skey，然后服务器在数据库中查找用户，如果存在就可以让用户进行下一步操作，如果不存在，则直接忽略或者返回验证失败的信息。具体代码如下
```javascrpt
//客户端
    wx.request({
      url: 'https://k3d2hspl.qcloud.la/weapp/xxx',
      method: 'POST',
      header: {
        "Content-Type": "application/x-www-form-urlencoded"
      },
      data: {
        skey: wx.getStorageSync('weapp_session_' + 'F2C224D4-2BCE-4C64-AF9F-A6D872000D1A'),
      }
	  ...
    })
```

```javascrpt
//服务器处理函数
		const body = ctx.request.body
        var userInfo = await AuthDbService.getUserInfoBySKey(body.skey).then((res) => { return res })
        if (userInfo.length < 1) {
            return
        }
		//do something you want here
```
其中```AuthDbService.getUserInfoBySKey(skey)```函数从表格中读取用户数据，如果存在用户则可以进行下一步操作，如果失败则直接忽略

### 获取影院
用户在客户端获取自己的定位并且根据[中华人民共和国行政区划代码](https://zh.wikipedia.org/wiki/%E4%B8%AD%E5%8D%8E%E4%BA%BA%E6%B0%91%E5%85%B1%E5%92%8C%E5%9B%BD%E8%A1%8C%E6%94%BF%E5%8C%BA%E5%88%92%E4%BB%A3%E7%A0%81)解析成provinceId、cityId以及blockId，并传给服务器，便可以获取到该地区的电影列表，具体代码细节如下：

```javascrpt
//服务器处理函数
		var sql = 'SELECT * FROM cinema LEFT JOIN locationUserOrCinema ON cinema.cinema_id=locationUserOrCinema.cinema_id \
			LEFT JOIN location ON locationUserOrCinema.location_id=location.location_id \
			WHERE province_id = ' + ctx.request.query.provinceId + \
			' AND city_id = ' + ctx.request.query.cityId + \
			' AND block_id = ' + ctx.request.query.blockId
		var result = await DB.raw(sql).then((res) => {
            return res
        })
        ctx.state.data = {
            resultCode: 0,
            values: result[0]
        }
```

其中```result[0]```包含了所有符合要求的电影数据

### 获取电影
这里获取电影有三种方式，一种是通过影院获取电影，一种是直接获取所有电影，一种是根据movie_id获取电影，这三种方式都在同一个控制器中，该控制器如下：

```javascrpt
const DB = require('./dbindex')
module.exports = {
    get: async ctx => {
        if (ctx.request.query.cinemaId) {
            var result = await DB.raw('SELECT * FROM movie LEFT JOIN cinemaMovie ON movie.movie_id=cinemaMovie.movie_id WHERE cinema_id = ' + ctx.request.query.cinemaId).then((res) => {
                return res
            })
        }
        else if (ctx.request.query.movieId) {
            var result = await DB.raw('SELECT * FROM movie WHERE movie_id = ' + ctx.request.query.movieId).then((res) => {
                return res
            })
        }
        else {
            var result = await DB.raw('SELECT * FROM movie').then((res) => {
                return res
            })
        }
        ctx.state.data = {
            resultCode: 0,
            values: result[0]
        }
    }
}
```

其中DB为一个knex实例，用于连接数据库，其他的操作跟获取电影院没什么差别

### 获取场次、座位以及电影院周边
跟获取影院和电影的实线差不多，在此不做赘述

### 订电影票
在选择了影院，电影，场次，座位以后，接下来就是订票了，在这个步骤我们考虑到用户可能在选票后还需要选择一些电影周边比如爆米花、可乐或者是电影周边公仔之类的附加商品，而用户在选择这些商品的时候需要消耗时间，短则几秒多则几分钟，所以在用户选票之后我们需要锁定这个座位，避免用户选择完附加商品之后票被“抢了”的情况。在这里我们通过改变seat的state的方法在标志这张票是被锁定的状态。而我们的设计是票“用时再创”的想法，因为没有必要在数据库初始化的时候创建所有的票。

创建的时候就会有一个序号的问题，在这个问题上我们采用了”最大号加1“的原则，也就是获取数据库中最大的序号，然后加1得到当前票的序号。

既然有锁定，对应的就会有解锁操作，在订单取消以及没创建订单的情况下就会发起释放票的操作。

其中锁定电影票的代码如下，取消锁定、获取订单里的票数据的函数类似

```javascript
const DB = require('./dbindex')
const AuthDbService = require('../node_modules/wafer-node-sdk/lib/mysql/AuthDbService')

module.exports = {
    create: async ctx => {
		//认证环节
		const body = ctx.request.body
        var userInfo = await AuthDbService.getUserInfoBySKey(body.skey).then((res) => { return res })
        var open_id = userInfo[0].open_id
        if (userInfo.length < 1) {
            return
        }
		//数据解析
        var cinema_id = body.cinemaId,
            movie_id = body.movieId,
            screening_id = body.screeningId,
            seat_id = body.seatId,
            price = body.price
		//判断座位状态
        var result = await DB('seat').select('*').where({
            cinema_id: cinema_id, movie_id: movie_id, screening_id: screening_id, seat_id: seat_id
        })
        if (result.length <= 0) {
            ctx.state.data = {
                resultCode: 1,
                resultDes: '没有这个座位',
            }
        }
        else if (result[0].state != 0) {
            ctx.state.data = {
                resultCode: 2,
                resultDes: '座位已被锁定',
            }
        }
        else {
			//锁定座位
            result = await DB('seat').where({
                cinema_id: cinema_id, movie_id: movie_id, screening_id: screening_id, seat_id: seat_id
            }).update({ state: 1 })
            var ticiets = await DB('ticket').select('*').orderBy('ticket_id', 'desc')
			//获取当前应该的id
            var ticket_id
            if (ticiets.length <= 0) {
                ticket_id = 0
            }
            else {
                ticket_id = ticiets[0].ticket_id + 1
            }
            result = await DB('ticket').insert({
                ticket_id, cinema_id, movie_id, screening_id, seat_id, price, open_id
            })
            ctx.state.data = {
                resultCode: 0,
                resultDes: 'success',
                ticket_id: ticket_id
            }
        }
    }
}
```

### 订单相关操作
在选择完了电影票和周边产品之后，我们就需要提交订单正式获取到商品。订单的操作有新建、取消、获取以及支付操作。

其中在数据库生成一个订单是一个十分简单的事情，我们真正需要考虑的是如何在关系表中添加关系，在这里我们的设计是，在创建一个订单之后，在ticketOrder中添加与之关联的票，并在itemOrder中添加与之关联的周边商品。具体代码跟电影票操作类似，故不赘述。

### 拓展及改进
待开发

## 项目管理方面
在项目管理上，作为一个项目经理，首先要自我检讨一下，我没有能很好地动员自己的团队，进而导致分配的任务没有被很好的完成，这是一个十分需要检讨的地方。