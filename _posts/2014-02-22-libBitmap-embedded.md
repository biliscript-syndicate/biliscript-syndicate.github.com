---
layout: post
title: "播放器更新：内嵌libBitmap"
author: nekofs
description: ""
category: update
tags: []
---
{% include JB/setup %}

player.swf **20140130** 。libBitmap库已内嵌入player.swf，无需再用`load()`加载造成额外延迟。以前使用`load`的代码仍然正常工作，可以看出更新时考虑了向以前兼容的问题。
