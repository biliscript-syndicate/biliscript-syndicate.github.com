---
layout: post
title: "播放器安全更新总结"
author: nekofs
description: ""
category: update
tags: []
---
{% include JB/setup %}

player.swf **20151029** 。并没有功能更新。观看了第二届弹幕大赛后，我深受启发，查阅了从上个帖子至今近两年58个play.swf更新版本，在此证实确无功能上的更新（好像没什么用）。安全更新包括（2015年8月14日）：禁止了`__scope`属性的访问；关闭了`with`语法关键词的解析，现在会产生异常“不能使用 with!”。
