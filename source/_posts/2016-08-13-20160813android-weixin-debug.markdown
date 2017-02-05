---
author: xsstomy
date: 2016-08-13 20:28:39+00:00
layout: post
title: 手机微信端调试
pid: 18
tags:
- reactjs
- 微信
- 调试
---

## 前言
最近使用reactjs开发单页应用，主要使用reactjs + webpack + redux + es2015(es6),因为使用了es2015 ，由于兼容性的问题，遇到一次比较坑的爬坑经历。情况是这样的，发布单页过后，在苹果手机微信中打开都是正常，在其他浏览器(chrome,safari)也是正常的；在安卓微信中都打不开,但是在chrome,qq浏览器也是正常的。当时就懵逼了，当时心里的状态是这样的，我靠，这是尼玛什么情况。没有办法，只能找办法调试解决了，但是要调试微信中的啊，其它浏览器中都是正常的啊，这时真是尴尬，完全不知道该如何调试手机端的微信(求心里阴影面积)。因为只在微信中出现，chrome中是正常的，那就不能使用chrome 调试方式了。这里是电脑调试手机端chrome方式[谷歌官方文档](https://developers.google.com/web/tools/chrome-devtools/debug/remote-debugging/remote-debugging)，再贴一个中文的[文档教程]()。最后找到微信web 开发者工具，最终调试成功。最终调试才知道是Object.assign 的兼容性问题，最后使用了[object-assign](https://www.npmjs.com/package/object-assign) 来解决兼容性的问题。下面来写一下这一次的详细调试过程。


## 调试工具 
- [微信web开发者工具](https://mp.weixin.qq.com/wiki/10/e5f772f4521da17fa0d7304f68b97d7e.html)
- 安卓手机一部
- 主要用到x5 blink 内核调试方式

## 步骤


1.前面的可以看官方的文档,按照微信官方文档中的准备工作做好，然后把安卓手机微信中X5 blink 的设置也设置好。然后分别重启手机中的微信和pc的微信web开发者工具。(这里被坑了一下，开始的时候死活不能调试，分别重启了一下手机和web开发者工具就可以调试了)

这里是微信的开始调试之前的准备工作步骤，[微信官方文档地址](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1455784140&token=&lang=zh_CN)


![](/uploads/2016/08/13/weixin-debug-ready.png)


这里贴一张我这里未开始调试的图


![](/uploads/2016/08/13/debug-start.png)


2.开始调试，请确保手机和微信web开发者工具都配置好，然后在web开发者工具中，选择X5 blink 调试， 然后就会弹出一个界面(移动调试，设备列表)， 如下图

![](/uploads/2016/08/13/weixin-debug-start.png)

这里是官方文档的图。

因为我这里没有安卓手机，所以只能先大概的文字描述一下。会有三种调试方式，一个chrome调试方式，一个是X5  blink调试方式，一个是代理的调试方式。这里我们要用的是X5 blink 调试。点击com.tencent.mm 下面的网页inspect，这时候我们就可以调试手机端的微信里面页面了，直接源码调试，可以查看各种源码了，还可以断点调试。

![](/uploads/2016/08/13/weixin-debug-debuging.png)


调试到这里基本就结束了，主要是调试的方式，微信web开发者工具还是不错的，可以直接远程调试手机端微信里面的网页了，不像以前只能alert调试，想想就好伤痛。


![](/uploads/mypictures/xsstomyzhifubao.png)
