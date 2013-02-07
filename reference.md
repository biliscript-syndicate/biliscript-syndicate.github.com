---
layout: post
title: "API 速查手册"
description: ""
category: 
tags: []
---
{% include JB/setup %}

## API 速查手册

### 运行时

* **trace**(... args):void

* **clear**():void

* $G, Global
  * **\_set**(name:String, value:\*):void
  * **\_**, **\_get**(name:String):\*

* ScriptManager
  * **clearTimer**():void
  * **clearEl**():void
  * **clearTrigger**():void
  * *pushTimer(param1:Timer):void*
  * *popTimer(param1:Timer):void*
  * *pushEl(param1:IMotionElement):void*
  * *popEl(param1:IMotionElement):void*

* **load**(library:String, onload:Function):void  
  只有`libBitmap`可用。只在加载成功时调用onload。

### 语言

* **foreach**(object:Object, iterator:Function):void (Utils.foreach)  
  只能访问公开可遍历属性。

* **clone**(object:\*):\* (Utils.clone)  
  有些（TODO）类型无法正确复制

### 数据转换
* Utils

  * **hue**(value:int):int  
    TODO
  * **rgb**(r:int, g:int, b:int):int  
    TODO `r << 16 | g << 8 | b` ?
  * **formatTimes**(second:Number):String  
    时间格式mm:ss
  * **rand**(min:Number, max:Number):Number
  * **distance**(x1:Number, y1:Number, x2:Number, y2:Number):Number

### 播放器信息 

* Player
  * **state**:String
  * **time**:Number
  * **width**, **height**:uint
  * **videoWidth**, **videoHeight**:uint
  * **commentList**:Array

* $, Display
  * **fullScreenWidth**, **fullScreenHeight**:uint
  * **width**, **height**:uint
  * _**screenWidth**, **screenHeight**:uint_
  * _**stageWidth**, **stageHeight**:uint_

### 播放器控制

* Player
  * **play**():void
  * **pause**():void
  * **seek**(time_msec:Number):void
  * **jump**(av:String, page:int = 1, newwindow:Boolean = false):void
  * **commentTrigger**(onComment:Function, timeout_msec:Number = 1000):uint
  * **keyTrigger**(onKey:Function, timeout_msec:Number = 1000, up:Boolean = false):uint
  * **setMask**(mask:DisplayObject):void
  * **createSound**(name:String, onload:Function = null):ScriptSound
  * **refreshRate**:int

* $, Display

  * _root:Sprite_

### 接口包装

<table class="table table-bordered table-condensed">
<tbody>
<tr><td rowspan="7">(Top Level)</td><td>Math</td><td rowspan="4"></td><td>Math</td></tr>
<tr><td>String</td><td>String (fromCharCode)</td></tr>
<tr><td>parseInt()</td><td>parseInt</td></tr>
<tr><td>parseFloat()</td><td>parseFloat</td></tr>
<tr><td>Vector.&lt;int&gt;()</td><td rowspan="3">$, Display</td><td>toIntVector(a:Array)</td></tr>
<tr><td>Vector.&lt;uint&gt;()</td><td>toUintVector(a:Array)</td></tr>
<tr><td>Vector.&lt;Number&gt;()</td><td>toNumberVector(a:Array)</td></tr>


<tr><td rowspan="5">flash.display</td><td>BitmapData()</td><td rowspan="2">Bitmap</td><td>createBitmapData</td></tr>
<tr><td>Bitmap()</td><td>createBitmap, createParticle</td></tr>
<tr><td>TextField()</td><td rowspan="3">$, Display</td><td>createTextField, createComment</td></tr>
<tr><td>Sprite()</td><td>createCanvas, createButton</td></tr>
<tr><td>Shape()</td><td>createShape</td></tr>

<tr><td rowspan="14">flash.filters</td><td>BevelFilter()</td><td rowspan="14">$, Display</td><td>createBevelFilter</td></tr>
<tr><td>BitmapFilter()</td><td>?</td></tr>
<tr><td>BitmapFilterQuality</td><td>(DIY)</td></tr>
<tr><td>BitmapFilterType</td><td>(DIY)</td></tr>
<tr><td>BlurFilter()</td><td>createBlurFilter</td></tr>
<tr><td>ColorMatrixFilter()</td><td>createColorMatrixFilter</td></tr>
<tr><td>ConvolutionFilter()</td><td>createConvolutionFilter</td></tr>
<tr><td>DisplacementMapFilter()</td><td>createDisplacementMapFilter</td></tr>
<tr><td>DisplacementMapFilterMode</td><td>(DIY)</td></tr>
<tr><td>DropShadowFilter()</td><td>createDropShadowFilter</td></tr>
<tr><td>GlowFilter()</td><td>createGlowFilter</td></tr>
<tr><td>GradientBevelFilter()</td><td>createGradientBevelFilter</td></tr>
<tr><td>GradientGlowFilter()</td><td>GradientGlowFilter</td></tr>
<tr><td>ShaderFilter()</td><td>?</td></tr>

<tr><td rowspan="10">flash.geom</td><td>ColorTransform()</td><td rowspan="6">$, Display</td><td>createColorTransform</td></tr>
<tr><td>Matrix()</td><td>createMatrix, createGradientBox</td></tr>
<tr><td>Matrix3D()</td><td>createMatrix3D</td></tr>
<tr><td>Orientation3D()</td><td>(DIY)</td></tr>
<tr><td>PerspectiveProjection()</td><td>?</td></tr>
<tr><td>Point()</td><td>createPoint</td></tr>
<tr><td>Rectangle()</td><td>Bitmap</td><td>createRectangle</td></tr>
<tr><td>Transform()</td><td rowspan="3">$, Display</td><td>?</td></tr>
<tr><td>Utils3D</td><td>n/a</td></tr>
<tr><td>Vector3D()</td><td>createVector3D</td></tr>

<tr><td rowspan="5">flash.utils</td><td>clearTimeout()</td><td rowspan="3"></td><td>clearTimeout</td></tr>
<tr><td>getTimer()</td><td>getTimer</td></tr>
<tr><td>setTimeout()</td><td>timer</td></tr>
<tr><td>ByteArray()</td><td>bitmapData</td><td>getPixels</td></tr>
<tr><td>Timer()</td><td></td><td>interval</td></tr>

<tr><td>org.libspark.betweenas3</td><td>BetweenAS3</td><td></td><td>Tween</td></tr>
</tbody>
</table>
