---
layout: post
tags: homework
title: "Software System Analysis and Design HW8"
---
系统分析与设计的第八次作业.

## 软件架构与框架之间的区别与联系
软件架构是关于软件如何设计的一个重要的策略，软件的架构设计涉及到将软件分解成不同的部分，各部分之间有静态的结构关系，也有动态的交互关系。软件架构是语言无关的，只关乎到软件的结构设计方面。

而软件框架通常是只我们用一种特定的语言来实现我们之前的设计，比如说.net Framework就是一个已经实现的框架，里面按照架构师所设计的架构进行结构分层，建立不同部分之间的联系。

也就是说，架构设计是框架设计的指南，框架是架构落实到某种语言的确切代码的实现。

## 程序架构

### 三层架构模型图
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw8/layers.png?raw=true">
</center>

### 三层架构设计给程序员带来的方便之处
三层架构设计所带来的方便之处，其实就是分层给程序员带来的好处。首先最直观的好处就是我们只需要专注于自己负责的那部分的逻辑代码的实现，至于其他关联的层，只需要了解一下函数接口的调用以及调用结果的处理，这样就使得一个软件能够被分解为多个相对独立的模块去实现，大大缩减了项目中程序员沟通的时间。比如我负责这个软件的持久化层，我就只需要写好一个模块，这个模块有各个对数据库进行增删改查的函数，然后我只需要实现并说明这些函数，而完全不需要管别人会用这些函数做什么，这就大大增强了模块间的独立性。

再者，三层架构设计也可以使得程序员可以更快地了解一个软件的结构和各个结构的分工，也缩减了融入该项目所花费的时间成本。比如分层之前，面对一个比较大的软件的时候，我们可能很迷茫不知道自己需要做些什么，但是分层之后，我们可以很清晰地了解到我们需要做的那一小块的东西是什么，上手起来就很容易了。

以及，符合三层架构的软件维护起来更加地容易，因为非常容易就能检查出是哪一层出现了错误，交由开发该层的程序员去解决，这样可以更快地修复错误，也可以降低维护的成本。比如在我们的软件中，当我们发现我们的持久化层比较慢的时候，我们便可以只改进这一个层的代码，甚至可以进行重构，而不影响到其他层的代码和结构。

## VUE 与 Flux 状态管理的异同
##### Flux
- Flux是一种架构思想，它将一个应用分成四个部分
	- View：视图层
	- Action(动作)：视图层发出的消息
	- Dispatcher(派发器)：用来接收Actions，执行callback function，类似于路由器
	- Store(数据层)：用来存放应用的状态，一旦状态变动则通知View进行更新

他们之间的状态如下图所示：
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw8/fluxstatemanagement.png?raw=true">
</center>

Flux 实现了数据的“单向流动”

View -> Action -> Dispatcher -> Store -> View Change

##### Vue.js
Vue.js是一款流行的JavaScript前端框架，Vue提供Vuex来实现状态管理。而Vuex有着一种“类Flux状态管理”的实现。

可以说Vue.js是Flux的一种实现。所以Vuex的状态管理方法实现了Flux中的状态管理方法，也就是上述Flux的方法，引用Vue官方的一张图：
<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/ssaad_hw8/vuestatemanagement.png?raw=true">
</center>

##### 相同
由于Vuex是基于Flux架构实现的，所以两者在状态管理方面有着很大的相似性，比如对于数据的处理都是单向流动，包括传输、更新的动作都是一致的。

##### 差异
但是实现起来总是跟理论的架构有所差距的。Vue.js使用mutations来实现状态的同步更新，如下

View -> Mutation -> Dispatcher -> Store -> View Change

但是Vuex又使用了Action来实现异步操作，如下

View -> Action -> Mutation -> Dispatcher -> Store -> View Change

其实这个差别是非常小的，而且Action也不是一个必须的东西，因为所有的操作其实最后都要由Mutation来执行，引用Vue.js作者尤雨溪的一句话

>事实上在 vuex 里面 actions 只是一个架构性的概念，并不是必须的，说到底只是一个函数，你在里面想干嘛都可以，只要最后触发 mutation 就行。异步竞态怎么处理那是用户自己的事情。vuex 真正限制你的只有 mutation 必须是同步的这一点（在 redux 里面就好像 reducer 必须同步返回下一个状态一样）。