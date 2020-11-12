---
title: jar包冲突
date: 2020-11-04 22:27:02
categories: 
    - 日常比较
tags: 
    - 开发环境
---

&nbsp;&nbsp;明天需要上线需求，所以准备和代码。下班的时候群里就有同事反馈，pre_master分支起不来，直到我准备和代码的时候已经过去2个小时，群里没有动静，心想问题应该已经处理了。为了保险起见还是跑了一遍代码。我擦，没人处理，2个小时过去了，代码一直有人往上和，就是没人处理起不来的问题。好吧，我先看下什么问题吧。。

从报错看在加载rpc client类时报错，看着像resty-pass的jar包的问题，想起有同事升级这个jar的版本的需求，就翻看了jar的说明文档，里面明确提出，升级到6以上的版本，需要注意netty-common的版本需要与之对应。

{% asset_img  启动失败.jpg [启动失败.jpg] %}

通过maven helper工具 发现，确实工程中存在两个版本的netty-common，联系同事，处理问题。搞定，和代码睡觉。

睡觉之前顺便，写一下 __如何处理jar冲突__

### 1.下载idea插件 maven helper

这个就不用太细节了，如下图

{% asset_img maven插件.png [maven插件.png] %}


### 2.插件的使用

进入pom文件，会发现，走下角多个一个tab,这个就是maven helper的界面

界面有三个选项：

Conflicts（查看冲突）
All Dependencies as List（列表形式查看所有依赖）
All Dependencies as Tree（树形式查看所有依赖）
{% asset_img 界面.png [界面.png] %}



### 3.当出现冲突jar时，右击可以进行处理

当然，处理jar包，还是需要进行评估下，是否会对系统的功能有影响，不能盲目的一顿操作。











