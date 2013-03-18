---
layout: post
title: "播放器更新：$.frameRate"
description: ""
category: update
tags: []
---
{% include JB/setup %}

player.swf **20130318** 默认帧率从60改回24。增加`$.frameRate`接口，样例：`$.frameRate = 60; trace($.frameRate);`。

之前发现60帧仍然存在弹幕运动不连贯的状况。播放器也许跑不到60帧。
