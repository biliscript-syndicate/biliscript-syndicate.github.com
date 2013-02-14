---
layout: page
title: "速查手册"
author: nekofs
description: ""
group: navigation
style: "body { font-size: 13px; line-height: 16px;} li { line-height: 16px;}"
---
{% include JB/setup %}

{% assign asdoc = 'http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3' %}
{% assign utils = asdoc | append: '/flash/utils' %}

## API

<div markdown="1" class="row">
<div class="span6">
### 基本操作

* **clear**():void
* **clone**(object:\*):\*  
  (Utils.clone) 有些（TODO）类型无法正确复制
* **foreach**(object:Object, iterator:Function):void  
  (Utils.foreach) 只能访问公开可遍历属性。例`foreach({1:2, 3:4}, function(key, value) {trace(key, value);});`
* **load**(library:String, onload:Function):void  
  只有`libBitmap`可用。只在加载成功时调用onload。例`load('libBitmap', function(){trace('ok', Bitmap);});`
* **trace**(... args):void  
  例`trace(1, 2, [3,4], '5 6', trace);`
* $G.**\_get**(name:String):\*  
  ($G.\_, Global.\_get, Global.\_)
* $G.**\_set**(name:String, value:\*):void  
  (Global.\_set)
* ScriptManager.**clearEl**():void  
  停止并清除$.createComment()、$.createShape()、$.createCanvas()、$.createButton()、Bitmap.createBitmap()产生的运动元件。
* ScriptManager.**clearTimer**():void  
  清除只由interval()产生的计时器。不清除timer()。
* ScriptManager.**clearTrigger**():void  
  清除只由Player.keyTrigger()产生的键盘事件侦听。不清除Player.commentTrigger()。

### 时间

* **[clearTimeout]({{utils}}/package.html#clearTimeout%28%29)**(timeout_id:uint)  
  中止由timeout_id指定的延时操作。
* **[getTimer]({{utils}}/package.html#getTimer%28%29)**():int  
  毫秒
* **interval**(exec:Function, delay_msec:Number = 1000, repeatCount:uint = 1):[Timer]({{utils}}/Timer.html)  
  (Utils.interval) 重复定时执行。repeatCount为0则无限重复。delay推荐最小20毫秒（再小影响性能）。
* **timer**(exec:Function, delay_msec:Number = 1000):uint  
  (Utils.delay) 一次延时执行。delay最小1毫秒。返回timeout_id。

### 数据转换

* **[parseInt]({{asdoc}}/package.html#parseInt%28%29)**(str:String, radix:uint = 0):Number
* **[parseFloat]({{asdoc}}/packate.html#parseFloat%28%29)**(str:String):Number
* $.**toIntVector**(ints:Array):[Vector]({{asdoc}}/Vector.html).&amp;lt;int&amp;gt;
* $.**toUintVector**(uints:Array):[Vector]({{asdoc}}/Vector.html).&amp;lt;uint&amp;gt;
* $.**toNumberVector**(numbers:Array):[Vector]({{asdoc}}/Vector.html).&amp;lt;Number&amp;gt;
* String.**[fromCharCode]({{asdoc}}/String.html#fromCharCode%28%29)**(... charCodes):String  
  Unicode码。例`trace(String.fromCharCode(27979, 35797, 10, 9731, 9773));`
* Utils.**distance**(x1:Number, y1:Number, x2:Number, y2:Number):Number  
  即`Math.sqrt((x1 - x2)*(x1 - x2) + (y1 - y2)*(y1 - y2))`
* Utils.**formatTimes**(second:Number):String  
  时间格式mm:ss；例`trace(Utils.formatTimes(Player.time / 1000));`
* Utils.**hue**(value:int):int  
  最小0 ![色谱](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAWgAAAAICAIAAABbBPJsAAAAZ0lEQVR42u3UMQqAMBAEwDUvT+G7E61EBFGJ6WY4LIIeG4tdkl7TlvTLlP15N2PvP38yJ89zmLl5akv6Mev/QdtdoPLT/vHl8+9bS9Lq+ciPnpGnBOAjxQEoDkBxAIoDUByA4gB4YwNtkWicaN4UaAAAAABJRU5ErkJggg==) 最大359
* Utils.**rand**(min:Number, max:Number):Number  
  整数，即`Math.floor(min + Math.random() * (max - min))`
* Utils.**rgb**(r:int, g:int, b:int):int  
  耗时是 `r &lt;&lt; 16 | g &lt;&lt; 8 | b` 的2倍。

### 几何

{% assign geom = asdoc | append: '/flash/geom' %}

无法获得Utils3D。详细参数见Adobe手册页面。

* $.**createColorTransform**(...):[ColorTransform]({{geom}}/ColorTransform.html)
* $.**[createGradientBox]({{geom}}/Matrix.html#createGradientBox%28%29)**(...):[Matrix]({geom}}/Matrix.html)  
  即`(new Matrix()).createGradientBox(...)`。用于beginGradientFill()和lineGradientStyle()。
* $.**createMatrix**(...):[Matrix]({{geom}}/Matrix.html)
* $.**createMatrix3D**(...):[Matrix3D]({{geom}}/Matrix3D.html)
* **[PerspectiveProjection]({{geom}}/PerspectiveProjection.html)**  
  `clone($.root.transform.perspectiveProjection)`
* $.**createPoint**(x:Number = 0, y:Number = 0):[Point]({{geom}}/Point.html)
* **[Rectangle]({{geom}}/Rectangle.html)**  
  `$.root.getRect(null)`或`Bitmap.createRectangle(x, y, w, h)`
* $.**createVector3D**(...):[Vector3D]({{geom}}/Vector3D.html)

### 库

* **[Tween](http://www.libspark.org/wiki/BetweenAS3/en)**  
  (org.libspark.betweenas3::BetweenAS3)
* **[Math]({{asdoc}}/Math.html)**

</div>
<div class="span6">

### Player信息

* Player.**videoWidth**:uint, Player.**videoHeight**:uint \[只读\]  
  视频等比例尺寸
* $.**width**:uint, $.**height**:uint \[只读\]  
  (Player.width:uint, Player.height:uint) 播放窗口尺寸；包括黑边
* $.**stageWidth**:uint, $.**stageHeight**:uint \[只读\]  
  Flash界面尺寸
* $.**screenWidth**:uint, $.**screenHeight**:uint \[只读\]  
  ($.fullScreenWidth:uint, $.fullScreenHeight:uint) 屏幕尺寸
* Player.**commentList**:Array \[只读\]  
  一组[CommentData](#CommentData)。
* Player.**state**:String \[只读\]  
  `stop`, `pause`, `playing`
* Player.**time**:Number \[只读\]  
  毫秒

### Player控制

* Player.**commentTrigger**(onComment:Function, timeout_msec:Number = 1000):uint  
  返回timeout_id。不能用clearTimeout或者ScriptManager清除。
  例`Player.commentTrigger(function(c){trace(c, c.text);}, 1 &lt;&lt; 30);`
* Player.**createSound**(sample:String, onload:Function = null):ScriptSound  
  还不知道有什么采样可用。
* Player.**jump**(av:String, page:int = 1, newwindow:Boolean = false):void
* Player.**keyTrigger**(onKey:Function, timeout_msec:Number = 1000, up:Boolean = false):uint  
  timeout最大2147483647，小于0不工作。返回timeout_id。[查看样例](#Player.keyTrigger-example)。
* Player.**pause**():void
* Player.**play**():void
* Player.**refreshRate**:int  
  不工作；暂不修复，60帧可用。
* Player.**seek**(time_msec:Number):void  
  只能seek到关键帧。
* Player.**setMask**(mask:DisplayObject):void  
  即`player.parent.mask = mask;`

### 图形元件

{% assign disp = asdoc | append: '/flash/display' %}

以下通用参数（附默认值）：`{x:0, y:0, z:null, scale:1, alpha:1,`  
`parent:$.root, lifeTime:3, motion:{}}`

* $.**createButton**(params:Object):[CommentButton](#CommentObjects)  
  `{text:"Button", width:60, height:30, onclick:undefined}`
* $.**createCanvas**(params:Object):[CommentCanvas](#CommentObjects)  
* $.**createComment**(text:String, params:Object):[CommentField](#CommentObjects)  
  `{color:0xffffff, font:"黑体", fontsize:25}`
* $.**createShape**(params:Object):[CommentShape](#CommentObjects)  
* $.**createTextField**():[CommentField](#CommentObjects)  
  不初始化
* $.**createTextFormat**(...):[TextFormat]({{asdoc}}/flash/text/TextFormat.html)

### Bitmap库

* Bitmap.**createBitmap**(params:Object):[CommentBitmap](#CommentObjects)  
  `{bitmapData:undefined, pixelSnapping:"auto", smothing:undefined, scale:1}`
* Bitmap.**createBitmapData**(width:int, height:int, transparent:Boolean = true, fillColor:uint = 0xFFFFFFFF):[BitmapData]({{disp}}/BitmapData.html)
* Bitmap.**createParticle**(params:Object):[CommentBitmap](#CommentObjects)  
  TODO
* Bitmap.**createRectangle**(x:Number, y:Number, width:Number, height:Number):[Rectangle]({{geom}}/Rectangle.html)

### 滤镜

{% assign filt = asdoc | append: '/flash/filters' %}

无法获得ShaderFilter。详细参数见Adobe手册页面。
{% comment %}
trace(((Tween.tween($.root, {x:0})).updater).getObject('_shaderFilter'));

Doesn't work.

* (?) ShaderFilter(...)
{% endcomment %}

* $.**createBevelFilter**(...):[BevelFilter]({{filt}}/BevelFilter.html)
* $.**createBlurFilter**(...):[BlurFilter]({{filt}}/BlurFilter.html)
* $.**createColorMatrixFilter**(...):[ColorMatrixFilter]({{filt}}/ColorMatrixFilter.html)
* $.**createConvolutionFilter**(...):[ConvolutionFilter]({{filt}}/ConvolutionFilter.html)
* $.**createDisplacementMapFilter**(...):[DisplacementMapFilter]({{filt}}/DisplacementMapFilter.html)
* $.**createDropShadowFilter**(...):[DropShadowFilter]({{filt}}/DropShadowFilter.html)
* $.**createGlowFilter**(...):[GlowFilter]({{filt}}/GlowFilter.html)
* $.**createGradientBevelFilter**(...):[GradientBevelFilter]({{filt}}/GradientBevelFilter.html)
* $.**createGradientGlowFilter**(...):[GradientGlowFilter]({{filt}}/GradientGlowFilter.html)

### 内部

* $.**root**
* ScriptManager.**pushEl**(param1:IMotionElement):void
* ScriptManager.**popEl**(param1:IMotionElement):void
* ScriptManager.**pushTimer**(param1:Timer):void
* ScriptManager.**popTimer**(param1:Timer):void

</div>
</div>

--

## 类定义
<div markdown="1" class="row">
<div class="span6">
<a id="CommentData"> </a>
### CommentData

* **blocked**:Boolean
* **blockType**:uint
* **border**:Boolean
* **color**:uint
* **credit**:Boolean
* **danmuId**:uint \[只读\]
* **date**:String
* **deleted**:Boolean
* **id**:uint
* **mode**:uint
* **msg**:String
* **live**:Boolean
* **locked**:Boolean
* **on**:Boolean
* **pool**:int
* **preview**:Boolean
* **reported**:Boolean
* **size**:int
* **stime**:Number \[只读\] 秒
* **text**:String \[只读\]
* **type**:String
* **userId**:String \[只读\]

例`Player.commentList.forEach(function(e) {trace(e.stime, e.text);});`

<a id="MotionManager"> </a>
### MotionManager

TODO
* **running**:Boolean \[只读\]
* **reset**():void
* **play**():void
* **stop**():void
* **forcasting**(param1:Number):Boolean
* **setPlayTime**(param1:Number):void
* **initTween**(param1:Object, param2:Boolean = false):String
* **initTweenGroup**(motionGroup:Array, lifeTime:Number = NaN):void
* **setCompleteListener**(param1:Function):void

</div><div class="span6">

<a id="CommentObjects"> </a>
### Comment元件通用

* **motionManager**:MotionManager \[只读\]
* **initStyle**(params:Object):void  
  CommentBitmap除外
* **remove**():void

### CommentBitmap &rarr; [Bitmap]({{disp}}/Bitmap.html)

* **motionManager**:MotionManager \[读写\]
* **setParent**(parent:\*):void  
  即`parent.addChild(this)`

### CommentButton &rarr; [Sprite]({{disp}}/Sprite.html)

* **text**:String
* **fillColors**:Array
* **fillAlphas**:Array

### CommentCanvas &rarr; [Sprite]({{disp}}/Sprite.html)

### CommentField &rarr; [TextField]({{asdoc}}/flash/text/TextField.html)

{% assign tf = asdoc | append: '/flash/text/TextFormat.html' %}

* **[align]({{tf}}#align)**:String
* **[bold]({{tf}}#bold)**:Boolean
* **[font]({{tf}}#font)**:String
* **[fontsize]({{tf}}#size)**:uint
* **[color]({{tf}}#color)**:String
* **[htmlText]({{asdoc}}/flash/text/TextField.html#htmlText)**:String  
  过滤所有html

### CommentShape &rarr; [Shape]({{disp}}/Shape.html)

</div>
</div>

--

## 样板代码

<div markdown="1" class="row">
<div class="span6">

<a id="Player.keyTrigger-example"> </a>
### Player.keyTrigger

    Keysym = {65: 'A', 68: 'D', 83: 'S', 87: 'W'};
    var keyPressed = {};
    ScriptManager.clearTrigger();
    clearTimeout(Player.keyTrigger(function(keyCode) {
        keyPressed[Keysym[keyCode]] = true;
    }));
    clearTimeout(Player.keyTrigger(function(keyCode) {
        keyPressed[Keysym[keyCode]] = false;
    }, 1000, true));
    ScriptManager.clearTimer();
    interval(function() {
        trace('Key A is', keyPressed.A ? 'pressed.' : 'not pressed.');
    }, 100, 100);
    //Press A and observe debug console

### 鼠标定位

`trace($.root.mouseX, $.root.mouseY);`或者：

    var c = $.createComment('+', {lifeTime:0});
    c.transform.matrix3D = null;
    c.bold = false;
    var canvas = $.root;
    canvas.graphics.beginFill(0, 0);
    canvas.graphics.drawRect(0, 0, $.width, $.height);
    canvas.graphics.endFill();
    canvas.mouseEnabled = true;
    canvas.addEventListener('mouseMove', function (e) {
        c.x = e.localX - c.width / 2;
        c.y = e.localY - c.height / 2;
    });

</div><div class="span6">

### Bitmap库加载

    function startApplication() {
        var bmd = Bitmap.createBitmapData(40, 30, false, 0xffffff);
        var bmp = Bitmap.createBitmap({bitmapData:bmd, lifeTime:0, scale:2});
    }
    var loadText = $.createComment('加载Bitmap库，稍候…', {lifeTime:0, fontsize:14});
    loadText.transform.matrix3D = null;

    var loadTimeout = timer(function() {
        loadText.text = '载入超时，请刷新重试或检查网络连接。';
    }, 5000);
    load('libBitmap', function() {
        clearTimeout(loadTimeout);
        loadText.remove();
        startApplication();
    });

### 遍历显示列表

    function getChildren(path, node) {
        trace('[' + path + ']', node);
        if (!node.hasOwnProperty('numChildren')) return;
        for (var i = 0; i &lt; node.numChildren; i++)
            getChildren(path.concat(i), node.getChildAt(i));
    }
    getChildren([], $.root);

    function getChildFrom(root, path) {
        if (!path.length) return root;
        return getChildFrom(root.getChildAt(path.shift()), path);
    }
</div>
</div>

--

## 已知问题

(TODO: 扩充重现方法和结果)

* 安全考虑，TextField.htmlText被去掉所有html。
* 安全考虑，.loaderInfo属性被禁止访问。
* UI控制考虑，.root、.parent、.stage属性被禁止访问。
* Bitmap.createBitmap的smoothing参数被错别字成smothing。
* $.createComment、$.createShape、$.createCanvas、$.createButton会给进行DisplayObject.z = null导致产生一个Matrix3D导致图形模糊。解决方法`displayObject.transform.matrix3D = null;`。
* flash.display::Graphics里面没有cubicCurveTo方法，这是在FP11.0的特性（2011年10月）。
* 字符串中的`/n`会在提交后被转义成换行。
* `[]`访问符语法问题，无法嵌套`a = [0,1]; b = [0,1]; trace(a[0], b[a[0]]);`
