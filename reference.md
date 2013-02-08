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
  例`trace(1, 2, [3,4], '5 6', trace);`

* **clear**():void

* $G.**\_set**(name:String, value:\*):void (Global.\_set)

* $G.**\_get**(name:String):\* ($G.\_, Global.\_get, Global.\_)

* ScriptManager.**clearTimer**():void  
  停止并清除所有interval()产生的计时器。

* ScriptManager.**clearEl**():void  
  停止并清除$.createComment、$.createShape、$.createCanvas、$.createButton产生的MotionElement。

* ScriptManager.**clearTrigger**():void  
  清除所有Player.keyTrigger()产生的键盘事件侦听。

{% comment %}
These methods are public but only feasible for internal use.

* ScriptManager.**pushTimer**(param1:Timer):void

* ScriptManager.**popTimer**(param1:Timer):void

* ScriptManager.**pushEl**(param1:IMotionElement):void

* ScriptManager.**popEl**(param1:IMotionElement):void
{% endcomment %}

* **load**(library:String, onload:Function):void  
  只有`libBitmap`可用。只在加载成功时调用onload。

* **getTimer**():int  
  毫秒

* $.**root**  
  非公开

### Utils

* **foreach**(object:Object, iterator:Function):void (Utils.foreach)  
  只能访问公开可遍历属性。例`foreach({1:2, 3:4}, function(key, value) {trace(key, value);});`

* **clone**(object:\*):\* (Utils.clone)  
  有些（TODO）类型无法正确复制

* **timer**(exec:Function, delay_msec:Number = 1000):uint (Utils.delay)  
  delay最小为1。

* **clearTimeout**(id:uint)  
  提前结束延时，id由之前timer()返回。

* **interval**(exec:Function, delay_msec:Number = 1000, repeatCount:uint = 1):void (Utils.interval)  
  repeatCount为0则无限重复。delay推荐最小20（再小60fps运行不过来）。

* Utils.**hue**(value:int):int  
  TODO

* Utils.**rgb**(r:int, g:int, b:int):int   
  耗时是 `r << 16 | g << 8 | b` 的2倍。
{% comment %}
      N = 100000;
      rgb = Utils.rgb;
      var r, g, b, result;

      start = getTimer();
      var i = N;
      while (i--);
      trace('idle', (getTimer() - start) * 1000 / N, 'us/loop');

      start = getTimer();
      var i = N;
      while (i--)
          result = r << 16 | g << 8 | b;
      trace('manual', (getTimer() - start) * 1000 / N, 'us/loop');

      start = getTimer();
      var i = N;
      while (i--)
          result = rgb(r,g,b);
      trace('rgb()', (getTimer() - start) * 1000 / N, 'us/loop');

      //idle 0.87 us/loop
      //manual 2.47 us/loop
      //rgb() 4.16 us/loop
{% endcomment %}

* Utils.**formatTimes**(second:Number):String  
  时间格式mm:ss；例`trace(Utils.formatTimes(Player.time / 1000));`

* Utils.**rand**(min:Number, max:Number):Number  
  整数，即`Math.floor(min + Math.random() * (max - min))`

* Utils.**distance**(x1:Number, y1:Number, x2:Number, y2:Number):Number  
  即`Math.sqrt((x1 - x2)*(x1 - x2) + (y1 - y2)*(y1 - y2))`

### Player信息

{% capture table %}
Player.**videoWidth** | Player.**videoHeight** | 视频等比例尺寸
$.**width**           | $.**height**           | 播放窗口尺寸；包括黑边
Player.width          | Player.height          | 同上
$.**stageWidth**      | $.**stageHeight**      | 包括用户界面的尺寸
$.**screenWidth**     | $.**screenHeight**     | 屏幕尺寸
$.fullScreenWidth     | $.fullScreenHeight     | 同上
{% endcapture %}
{% include table %}

* Player.**state**:String  
  `stop`, `pause`, `playing`

* Player.**time**:Number  
  毫秒

* Player.**commentList**:Array


### Player控制

* Player.**play**():void

* Player.**pause**():void

* Player.**seek**(time_msec:Number):void  
  只能seek到关键帧。

* Player.**jump**(av:String, page:int = 1, newwindow:Boolean = false):void

* Player.**commentTrigger**(onComment:Function, timeout_msec:Number = 1000):uint

* Player.**keyTrigger**(onKey:Function, timeout_msec:Number = 1000, up:Boolean = false):uint

* Player.**setMask**(mask:DisplayObject):void  
  即`player.parent.mask = mask;`

* Player.**createSound**(sample:String, onload:Function = null):ScriptSound  
  还不知道有什么采样可用

* Player.**refreshRate**:int  
  不工作；暂不修复，60帧可用。

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
BitmapFilterQuality       | (自行枚举)
BitmapFilterType          | (自行枚举)
BlurFilter()              | $.createBlurFilter
ColorMatrixFilter()       | $.createColorMatrixFilter
ConvolutionFilter()       | $.createConvolutionFilter
DisplacementMapFilter()   | $.createDisplacementMapFilter
DisplacementMapFilterMode | (自行枚举)
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
Orientation3D           | (自行枚举)
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
<table class="table table-bordered table-condensed table-striped">
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
