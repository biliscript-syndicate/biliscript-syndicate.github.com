---
layout: page
title: "API 速查手册"
author: nekofs
description: ""
category: 
tags: []
---
{% include JB/setup %}

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

### 接口对照表

{% capture data %}
(Top Level)
Math                     | Math
String                   | String
parseInt()               | parseInt()
parseFloat()             | parseFloat()
Vector.&lt;int&gt;()     | $.toIntVector(a:Array):Vector.&lt;int&gt;
Vector.&lt;uint&gt;()    | $.toUintVector(a:Array):Vector.&lt;uint&gt;
Vector.&lt;Number&gt;()  | $.toNumberVector(a:Array):Vector.&lt;Number&gt;

flash.display
BitmapData() | Bitmap.createBitmapData
Bitmap()     | Bitmap.createBitmap
Bitmap()     | Bitmap.createParticle
TextField()  | $.createTextField
TextField()  | $.createComment
Sprite()     | $.createCanvas
Sprite()     | $.createButton
Shape()      | $.createShape

flash.filters
BevelFilter()             | $.createBevelFilter
BitmapFilter()            | (?)
BitmapFilterQuality       | (DIY)
BitmapFilterType          | (DIY)
BlurFilter()              | $.createBlurFilter
ColorMatrixFilter()       | $.createColorMatrixFilter
ConvolutionFilter()       | $.createConvolutionFilter
DisplacementMapFilter()   | $.createDisplacementMapFilter
DisplacementMapFilterMode | (DIY)
DropShadowFilter()        | $.createDropShadowFilter
GlowFilter()              | $.createGlowFilter
GradientBevelFilter()     | $.createGradientBevelFilter
GradientGlowFilter()      | $.createGradientGlowFilter
ShaderFilter()            | (?)

flash.geom
ColorTransform()        | $.createColorTransform
Matrix()                | $.createMatrix
Matrix()                | $.createGradientBox
Matrix3D()              | $.createMatrix3D
Orientation3D           | (DIY)
PerspectiveProjection() | (?)
Point()                 | $.createPoint
Rectangle()             | Bitmap.createRectangle
Transform()             | (?)
Utils3D                 | (n/a)
Vector3D()              | $.createVector3D

flash.utils
clearTimeout() | clearTimeout
getTimer()     | getTimer
setTimeout()   | timer
ByteArray()    | (?)
Timer()        | interval

org.libspark.betweenas3 http://www.libspark.org/wiki/BetweenAS3/en
BetweenAS3 | Tween
{% endcapture %}
{% assign rows = data | newline_to_br | strip_newlines | split: '<br />' %}
{% assign ASDOC = 'http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3' %}
<table class="table table-bordered table-condensed table-hover">
<tbody>
{% for row in rows %}
  {% if row != '' %}
    <tr>
    {% assign cells = row | split: '|' %}
    {% if cells.size == 1 %}
      {% if row contains '://' %}
        {% assign namespace = 'no doc' %}
        {% assign fields = row | split: ' ' %}
        <th colspan="3"><a href="{{fields[1]}}">{{fields[0]}}</a></th>
      {% else %}
        {% assign namespace = row | remove: '(Top Level)' | remove: ' ' %}
        {% if namespace != '' %}{% assign namespace = namespace | prepend: '.' %}{% endif %}
        <th colspan="3"><a href="{{ASDOC}}{{namespace | replace:'.','/'}}/package-detail.html">{{row}}</a></th>
      {% endif %}
    {% elsif namespace == 'no doc' %}
      <td>{{cells[0]}}</td><td>{{cells[1]}}</td>
    {% else %}
      <td>
      {% assign syms = cells[0] | split: '(' %}
      {% assign syms = syms.first | split: '.' %}
      {% assign sym = syms.first | remove: ' ' %}
      {% assign chars = sym | split: '' %}
      {% assign cap = chars.first | capitalize %}
      {% assign tail = cells[0] | remove_first: sym %}
        <a href="{{ASDOC}}{{namespace | replace:'.','/'}}/{% if cap == chars.first %}{{sym}}.html{% else %}package.html#{{sym}}{{tail}}{% endif %}">{{sym}}</a>{{tail}}
      </td>
      <td>
      {% assign syms = cells[1] | split: '(' %}
      {% assign tail = cells[1] | remove_first: syms.first %}
      {% assign syms = syms.first | split: '.' %}
      {% assign a = syms.first | remove: ' ' %}
      {% assign b = syms.last | remove: ' ' %}
        {% if a != '' %}<a href="#{{a}}">{{a}}</a>{% endif %}{% if syms.size > 1 %}.<a href="#{{b}}">{{b}}</a>{% endif %}{{tail}}
      </td>
    {% endif %}
    </tr>
  {% endif %}
{% endfor %}
</tbody>
</table>
