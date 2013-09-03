---
layout: page
title: "关于 / About"
description: ""
---
{% include JB/setup %}

Introduction
============

Biliscript is a programming language used in the scripting engine of [Bilibili](https://en.wikipedia.org/wiki/Bilibili) [Flash Player](https://static-s.bilibili.tv/play.swf). With the scripting engine, users and authors are able to create interactive subtitles, graphics, and games, enhancing the interactive experience of video playback.

Biliscript is a dialect of ECMAScript interpreted and run in the [BISE Scripting Engine](http://kinsmangames.wordpress.com/bise-scripting-engine/) VM, which is again written in ActionScript and run in the AVM, and supplmented with a subset of ActionScript runtime APIs. Through two layers of interpretion, the engine has very limited syntax and constrained performance, therefore it becomes an interesting challenge to create performance demanding applications within the restricted environment. An enthusiast community of Biliscript conducts regular research and contests around the language and engine.

[biliscript-syndicate.github.io](http://biliscript-syndicate.github.io) is a project to collect and document the details of the Biliscript engine and community created toolchains.


起因
====

最近在制作弹幕过程中有几个感想：

* &nbsp;经常需要查阅一些平凡重复的信息；
* &nbsp;无处了解之前弹幕艺术中使用的技术和想法，大量的代码没有文章介绍就死掉了；
* &nbsp;无法了解到弹幕播放器的最新状况；
* &nbsp;自己以前使用的一些方法未留文档记不清，又得重新想一遍。

这里主要希望实现这几件事情：

* &nbsp;整理提供需要经常查的一些方便信息；
* &nbsp;记录弹幕制作过程中的想法和技术，写成文档、教程，供参考；
* &nbsp;跟踪弹幕播放器的变化；
* &nbsp;介绍和评论以前的弹幕作品；
* &nbsp;跟踪弹幕艺术发展的近况。

联合文档，抛砖引玉。希望能有更多弹幕君在填坑时及时把想法捕捉保存下来。集中收集想法，相互启发，这就最好了。

github协作写作非常方便，参见[发表文章步骤](http://biliscript-syndicate.github.com/news/2013/02/13/submission-test.html)。
