---
title: 胡东炀
date: 2019-08-13 17:19:35
---

前端工程师
--------

* Phone: [18513886261](tel://18513886261)
* Email: <whudongyang@gmail.com>
* Github: [hudongyang](https://github.com/hudongyang)
* WeChat: whudongyang

个人信息
------

* 胡东炀 / 男 / 1986
* 江苏科技大学（ 2004 ～ 2008 ）
* 本科
* 工业工程

工作经历
------

* 小红唇（北京）网路科技有限公司（ 2016 / 4 ～ 至今 ）—— 前端架构师
* 北京怡合春天科技有限公司 （2015 / 6 ～ 2016 / 4 ）—— 前端工程师
* 北京品友互动信息技术有限公司（2013 / 4 ～ 2015 / 6 ）—— 前端工程师
* 北京牛仔网络科技有限公司 （ 2008 / 10 ～ 2013 / 4 ）—— Java 工程师

技能与专长
--------

以下分为**编程语言**、**标记或模板语言**、**框架**、**工具**等。比较擅长或平常使用较多的以^†^标记。

### 编程语言

- [Bash](https://zh.wikipedia.org/zh-hans/Bash)
- [Dart](https://dart.dev/)
- [Java](https://www.java.com/)
- [JavaScript](http://developer.mozilla.org/en/JavaScript) ^†^
- [Objective-C](https://en.wikipedia.org/wiki/Objective-C)
- [Swift](https://swift.org/)
- [TypeScript](https://www.typescriptlang.org/) ^†^

### 标记或模板语言

- [CSS](http://www.w3.org/Style/CSS/Overview.en.html) ^†^
- [EJS](https://ejs.co/) ^†^
- [HTML](http://developers.whatwg.org) ^†^
- [JSP](http://www.oracle.com/technetwork/java/javaee/jsp)
- [LESS](http://lesscss.org)
- [Markdown](http://daringfireball.net/projects/markdown)
- [Stylus](http://learnboost.github.io/stylus)

### 框架 / 库

- [axios](https://github.com/axios/axios) ^†^
- [Backbone.js](http://backbonejs.org)
- [dio](https://github.com/flutterchina/dio)
- [Express](http://expressjs.com)
- [Flutter](https://flutter.dev/)
- [jQuery](http://jquery.com) ^†^
- [Koa](https://koajs.com/) ^†^
- [Lodash](http://lodash.com) ^†^
- [mpvue](http://mpvue.com/) ^†^
- [Next](https://nextjs.org)
- [Nuxt.js](https://nuxtjs.org) ^†^
- [Node.js](http://nodejs.org) ^†^
- [React](http://facebook.github.io/react)
- [Require.js](http://requirejs.org) ^†^
- [scoped_model](https://github.com/brianegan/scoped_model)
- [Underscore.js](http://underscorejs.org) ^†^
- [Vue.js](https://vuejs.org) ^†^
- [Weex](https://weex.apache.org/zh/)
- [WePY](https://wepyjs.github.io/wepy-docs/)

### 工具

- [Apple XCode](http://developer.apple.com)
- [Charles](https://www.charlesproxy.com/)
- [Git](http://git-scm.com) ^†^
- [Grunt](http://gruntjs.com) ^†^
- [Gulp](http://gulpjs.com) ^†^
- [MySQL](http://mysql.com)
- [Nginx](http://wiki.nginx.org)
- [Sublime Text](http://www.sublimetext.com)
- [Visual Studio Code](https://code.visualstudio.com/) ^†^
- [webpack](https://webpack.js.org/)


项目经历
-------

### 素材管理系统
#### 简介
本项目是一个关于图片和视频的管理系统，运营人员将素材上传到腾讯 COS 后，客户可以查看素材，选择一些素材存入手机，并分享到朋友圈。 前端使用 React 进行开发，服务端是一个基于 koajs 的腾讯云 serveless 应用。

#### 职责

- 项目的技术负责人，前后端架构设计
- 项目的任务拆分和开发人员任务划分，估期
- 项目进度跟踪
- 腾讯云和 serveless 相关技术调研
- 采用 jwt 实现登陆
- 服务端的数据库设计、restful 接口实现
- 服务端的用户鉴权
- Koajs 中间件开发（cors, data, auth）


### 海报生成系统
#### 简介
该项目用于在小红唇 app 的商品详情页生成商品海报。该项目是一个 Node.js 项目，通过 [PhantomJS](https://phantomjs.org/) 对预定义的一个 h5 页面生成图片，再将该图片上传到阿里云 CDN 上，最后返回图片地址供 app 使用。

#### 职责
- 项目相关技术调研
- 由于生成图片是一个高 IO 的操作，在服务端实现一个队列，将请求放入队列中，以减轻服务器压力
- 监听队列里的 task，如果队列不为空，则从队列中取出一个任务执行
- 使用 Redis 对海报数据进行缓存，若 1 分钟之内对重复请求，直接从 Redis 中获取

### [小红唇商城 h5 项目](https://static.xiaohongchun.com)
#### 简介
这是一个商城项目，包括商品的浏览、购买、订单、个人中心、优惠券、会员等模块。基于 Koajs 和 Vue.js 开发。
#### 职责
- 项目的搭建及主要页面的开发
- 和 app 间的交互
- 使用 css-module 来防止 css 的 class name 去重
- base64 来编码项目 icon
- 使用 vuex 管理页面数据

### [梧桐会员管理后台](https://wutong.xiaohongchun.com)

#### 简介

该项目是一个基于最新的 [Next 9](https://nextjs.org) 开发的 h5 项目，使用 [TypeScript](https://www.typescriptlang.org/) 语言。server端使用 [Koa](https://koajs.com/) 定制，request库使用 [axios](https://github.com/axios/axios)。

#### 职责

- 技术调研及项目架构搭建
- 微信登陆和手机号绑定
- 公共组建开发
- 首页开发
- 鉴权中间件、日志中间件开发
- 线上环境部署及维护
- 微信公众号菜单设置及消息后台开发
- TS类型文件的定义

### [绝密花园管理后台](https://m.juemihuayuan.com/)

#### 简介

该项目使用 [Nuxt.js](https://nuxtjs.org) 开发，前端框架为 [Vue.js](https://vuejs.org) 。server端使用 [Koa](https://koajs.com/) 定制，request库使用 [axios](https://github.com/axios/axios)。

#### 职责

- 项目架构搭建
- 代码规范的制定并推行到团队
- 生产环境搭建及维护

### 天天跟我买

#### 简介

该产品是一个微信小程序，采用 [WePY](https://wepyjs.github.io/wepy-docs/) 和 [mpvue](http://mpvue.com/) 开发。

#### 职责

- 由于微信小程序原生语言固有的一些缺陷（比如不支持npm包管理），决定采用 [WePY](https://wepyjs.github.io/wepy-docs/) 框架开发。
- 埋点系统的设计及开发
- 商品详情页的接口重构
- 登陆
- 上线打包脚本的编写

### 小红唇 APP 商城首页 [Flutter](https://flutter.dev/) 重构

#### 简介

商城首页原来基于 [Weex](https://weex.apache.org/zh/) 开发，但由于以下原因，决定用 [Flutter](https://flutter.dev/) 重构

- [Weex](https://weex.apache.org/zh/) 本身在多平台上的表现差异很大，不得不写很多兼容性代码；而且不方便调试。
- 由于代码有移动端团队不熟悉 [JavaScript](http://developer.mozilla.org/en/JavaScript) 和 [Vue.js](https://vuejs.org) 的开发，代码的质量和可维护性差。
- 商城首页本身比较复杂且交互效果较多，使用原生开发成本很大。

#### 职责

- 对 [Flutter](https://flutter.dev/) 技术的调研
- 对项目用到的 Color、Image、Icon 进行集中管理，其中 Icon 使用 [IconFont](https://www.iconfont.cn) 管理。
- 请求库的 [dio](https://github.com/flutterchina/dio) 封装
- 状态管理使用的是 [scoped_model](https://github.com/brianegan/scoped_model)
- 由于商品列表是无限加载且类目需要悬停在顶部，使用了 CustomScrollView 和 SliverList 实现该效果
- [Flutter](https://flutter.dev/) 和 iOS 端的集成和相关 channel 的开发
- 和 Android 开发人员集成 [Flutter](https://flutter.dev/) 

### 小红唇微信消息同步和发送系统

#### 简介

提供消息的同步和发送接口给定时任务调用，给用户发送客服消息和模板消息。接收到请求后调用 [Java](https://www.java.com/) 微服务来完成相关操作。项目采用 [Koa](https://koajs.com/) 和 [TypeScript](https://www.typescriptlang.org/) 开发。

#### 职责
- [Koa](https://koajs.com/) 和 [TypeScript](https://www.typescriptlang.org/) 的开发环境搭建
- 相关接口和 [Java](https://www.java.com/) 微服务的开发
- 微服务调用使用 Service 层进行封装
- 微信模板和客服消息的数据封装




