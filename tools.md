---
layout: page
title: "工具"
description: ""
---
{% include JB/setup %}

### 弹幕塚

<http://code.google.com/p/danmaku-us/>

由[KPX](http://danmaku.us)开发，基于pmwiki的简易弹幕保存/离线开发工具。

KPX：“今年已经打算整个gpl放出来…不过目前也就把那边当git用没文字内容”。

### DanmakuHelper

由[面瘫半宅君](http://space.bilibili.tv/92776)和[音叉(Encode.X)](http://space.bilibili.tv/16425)共同开发的高级弹幕(Mode8)的绘图辅助工具。

详见[高级弹幕绘图助手：DanmakuHelper介绍](/news/2013/02/23/Danmaku-Helper.html)。

### BiliscriptToolkit

由[xarple](http://space.bilibili.tv/140964)开发的一系列工具集合。

详见[Biliscript Toolkit介绍](/news/2013/09/21/biliscript-toolkit.html)。

### SVG to Motifs Parser

Miller Medeiros的[SVG to Motifs Parser](http://blog.millermedeiros.com/converting-svg-to-five3d-flash-vector-graphics-and-html5-canvas/)，SVG到Graphics绘图指令的转换工具。EPM在《Round and Round》中[使用了这一工具](/news/2013/02/15/rnr-making-of.html)。

使用方式是将SVG源码填入”Input”框然后点击”Convert to AS3 Graphics”。其对SVG的遮罩、动画、样式表、文字、位图、渐变填充是缺乏支持的，作者使用的是Illustrator生成SVG。如果输入有不支持的东西会在”Warnings Panel”中显示。

### BitmapTool

[奇跡の海开发](http://9ch.co/t54582,1-1.html)，导入图像到Biliscript的工具。

<object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="550" height="400" id="hentai" align="middle">
<param name="movie" value="hentai.swf" />
<param name="quality" value="high" />
<param name="bgcolor" value="#ffffff" />
<param name="play" value="true" />
<param name="loop" value="true" />
<param name="wmode" value="window" />
<param name="scale" value="showall" />
<param name="menu" value="true" />
<param name="devicefont" value="false" />
<param name="salign" value="" />
<param name="allowScriptAccess" value="sameDomain" />
<!--[if !IE]>-->
<object type="application/x-shockwave-flash" data="/res/tools/hentai.swf" width="550" height="400">
    <param name="movie" value="hentai.swf" />
	<param name="quality" value="high" />
	<param name="bgcolor" value="#ffffff" />
	<param name="play" value="true" />
	<param name="loop" value="true" />
	<param name="wmode" value="window" />
	<param name="scale" value="showall" />
	<param name="menu" value="true" />
	<param name="devicefont" value="false" />
	<param name="salign" value="" />
	<param name="allowScriptAccess" value="sameDomain" />
<!--<![endif]-->
	<a href="http://www.adobe.com/go/getflash">
		<img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" alt="获得 Adobe Flash Player" />
	</a>
<!--[if !IE]>-->
</object>
<!--<![endif]-->
</object>


致谢：“主程序部分代码参考自Encode.X大大的线绘工具，bitmap类库实现方法参考自无成公子的相关文章，还有就是有问必答的面瘫大大”。

使用方法：

1. &nbsp;导入图片
2. &nbsp;如果是第一次使用，请勾选输出完整代码，并且给图片标识（命名规则遵循变量命名规则）
3. &nbsp;输出代码，将输出txt格式的文本文档，并以图片标识命名
4. &nbsp;打开txt代码文件后，部分代码不可直接复制，需要先进行自定义参数，文档里已经详细标注，这里不再罗嗦了
