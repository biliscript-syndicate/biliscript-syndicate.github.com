---
layout: post
title: "Bitmap库停止工作"
author: nekofs
description: ""
category: 
tags: []
---
{% include JB/setup %}

**更新**：20130216已修复。默认播放器域名还原至hdslb.com。

无法加载Bitmap库。

重现方法`load('libBitmap', function(){trace('ok', Bitmap);});`

实际结果：

    importExtendLibrary : libBitmap
    importExtendLibrary : libBitmap Downloading...
    Execute in 9ms
    importExtendLibrary : libBitmap Initalizing...
    importExtendLibrary : err ReferenceError: Error #1065

此库加载代码写死为从`http://static.hdslb.com/playerLibrary/libBitmap_2.swf`下载。查看网络流量未实际发出下载请求。默认播放器的链接变成了`http://static.loli.my/player.swf`，可能有跨域安全策略问题。
