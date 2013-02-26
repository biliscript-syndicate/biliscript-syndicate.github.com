---
layout: post
title : 弹幕涂鸦系统
tagline : 
author : nekofs
description : ""
category : 
tags : []
---
{% include JB/setup %}

我比较好奇，一个合作代码弹幕项目，会按怎样的过程进行下来，会经历多少情况。偶然一句话，产生了两周的工作，《弹幕涂鸦系统》。以下是[Xarple](http://space.bilibili.tv/140964)与我的合作项目制作日志。

![](/res/scratchpad-project-timeline/screenshot.png)

<!-- break -->

（标记：(x): Xarple；(n): nekofs）

##### 2013-02-14 21:02:17

如果在播放器上搞个涂鸦发送的话，类似百度贴吧的涂鸦，能够直接画图并发送，那样的话倒是个不错的方法。

##### 2013-02-15 可行性调研，产品分析，项目计划

一大堆涂鸦在那里飘过好像不是特别有趣味，找一个趣味点，这个有点难。看有没有视频内容吧，没有的话就搞个类似标签云那样的涂鸦云，一大堆涂鸦，不明觉厉。

这个价值在于观众突然有了一种新工具，会好玩一阵子。

难度在于怎么管理调度，一片乱糟糟全部盖上了，或者是缩小到看不清是啥。把图储存到队列里，延迟发送，每一定时间规定最多只能有N副飘过，控制厚度，遮挡检测？

##### 2013-02-16 实现原型1：传输编解码1(n)，实现原型2：笔触矢量化算法，三次贝塞尔拟合算法，界面，图形数据结构(x)，规范内部接口

##### 2013-02-17 完成传输编解码1(n)，修订图形数据结构(x)，实现界面(x)

因为调度制度的问题导致视频放完还有一大部分涂鸦没放完怎么办：就现在普通弹幕的处理方式也可以，不太多就调整之避免遮挡，如果太多也管不过来。

##### 2013-02-18 性能分析(n)，优化(x)，完成界面(x)

- &nbsp;优化：不再重复拟合已经确定的曲线段
- &nbsp;优化：不再重复计算弧长积分
- &nbsp;优化：使用Array.slice()避免循环
- &nbsp;（未实施）优化：主要渲染和计算放到enterFrame还是mouseMove？  
    结果：放在enterFrame图形会跳变不连续；性能压力下两者无实际区别。主要性能问题是Linux下鼠标事件过频繁。

##### 2013-02-19 优化(x)

- &nbsp;优化：不再重绘已经确定的图形。
- &nbsp;（未实施）优化：不计算因节点数过短而结果可预测的弧段  
    结果：因为Linux与Windows下事件处理模式相反，Windows下丢失事件保证延迟（因此必须计算短节点数弧段），Linux下保证事件增加延迟。

##### 2013-02-20 重写：传输编解码2(n)，自测(n)，协议实验(n)

##### 2013-02-21 完成弹幕调度算法(x)

- &nbsp;最终用什么视频？没有想法。曲包/作业用BGM

##### 2013-02-22 QA(n)，UI/UX(x)，修bug(x)

##### 2013-02-23 QA(n)，修bug(x)

##### 2013-02-24 开场制作(x)，QA(n)，修bug(x)

##### 2013-02-25 特效渲染(x)，压制(x)

##### 2013-02-26 上传(x)，发布测试(n,x)，QA通过(n)

##### 2013-02-27 发布(x)

________________________________________

##### 已完成任务

- BUG: \[\]问题  
    修复。
- BUG: Linux Flash鼠标事件太频繁劣化性能。重现：随便打开一个视频不播放，在上面晃动鼠标，cpu即满载。  
    无法修复。
- BUG: 0x01-0x19间的码字会被转换成空格  
    修复：重写传输组件。原因：XML标准规定NT-Char := #x9 | #xA | #xD | \[#x20-#xD7FF] | \[#xE000-#xFFFD] | \[#x10000-#x10FFFF]
- BUG: 无法同时显示多条弧线  
    修复。原因：整个Stage只能同时拥有24个有scrollRect的Bitmap 

      ScriptManager.clearEl();

      load("libBitmap", function() {
        shape = $.createShape({});
        $.root.removeChild(shape);

        canvas = $.createCanvas({});
        for (var i = 0; i < 30; ++i) {
          var bmp = Bitmap.createBitmap({parent:canvas, bitmapData:Bitmap.createBitmapData(500, 500, true, 0)});
          bmp.scrollRect = Bitmap.createRectangle(i, 0, 400, 400);
          shape.graphics.clear();
          shape.graphics.beginFill(0xffffff);
          shape.graphics.drawRect((i%10) * 35, ((i/10) ^ 0) * 35, 30, 30);
          shape.graphics.endFill();
          bmp.bitmapData.draw(shape);
        }
      });

- BUG: 操作一段时间后界面阴影filter自动消失  
    修复。原因：scrollRect把显示列表撑破了，所以不渲染filter了。
- BUG：进度条变化导致操作还原  
    修复。
- BUG：无法通过点击播放器中间控制视频播放/暂停  
    修复：.mouseEnabled = false。
- BUG: TextField跨平台baselineShift不一致。  
    无法修复。
- BUG: 复制按钮缺少颜色研所表示控制状态，用户无法有效使用  
    修复：不能复制的时候显示暗色、不显示鼠标动画。
- BUG: 进度条变化导致控制点辅助信息残留  
    修复。
- FEAT: UI/UX调整  
    完成。
- FEAT: ByteArray压缩  
    不实现。测试发现无实际效果。
- BUG: load()语法？  

      load('libBitmap', function() {
        [].forEach(function(){return;});
      });
      =====================================
      importExtendLibrary : libBitmap
      importExtendLibrary : libBitmap Downloading...
      Execute in 18ms
      importExtendLibrary : libBitmap Initalizing...
      importExtendLibrary : libBitmap create object...0
      importExtendLibrary : libBitmap done
      importExtendLibrary : null
      importExtendLibrary : null Downloading...
      extendLibraryLoadingError:[IOErrorEvent type="ioError" bubbles=false cancelable=false eventPhase=2 text="Error #2036"]
- BUG: 关闭所有trace调试信息  
    修复。
- BUG: 说明中应具有版本信息  
    修复。
- BUG: 无法处理多于3个涂鸦同时出现在同一纵行的情况，3个涂鸦被等距分布，其他涂鸦全部叠在一处  
    修复。
- FEAT: 阻止用户复制涂鸦数据重复发送  
    不修复。测试未发现性能可行性问题。
- FEAT: 可用空间为负的时候应该给复制按钮显示成灰色表示禁止复制  
    修复。
- FEAT: 调度器不解析mode，用户无法通过选择模式来控制涂鸦运动方式（mode4底部固定；mode5顶部固定）  
    修复。
- FEAT: 显示涂鸦信息以便up主管理  
    修复。
- BUG: 启动时未处理已经在$.root列表里的弹幕  
    修复。
- BUG: importExtendLibrary : err TypeError: Error #1009  
    修复。
- BUG: mode4/5初始化时没有处理  
    修复。
- BUG: 进度条变化后界面混乱/进度条变化导致闪过混乱界面  
    讨论seek判定条件，重现：在0秒处不断拉回0秒  
    NOTOURBUG: 播放器本身具有此问题  
    解决方法：ScriptManager.popEl()  
    修复。
- FEAT: 界面把mode4弹幕挡住了。所有mode4弹幕在显示界面时.y -= 10。  
    不修复。用户自己可以用“防止挡字幕”。
- FEAT: 用户友好地处理libBitmap加载失败的状况。  
    完成。
- FEAT: libBitmap超时后再加载成功拒绝继续执行  
    完成。
- FEAT: loading画面至少保持1秒  
    完成。
- FEAT: 开场弹幕隐藏（.alpha=0.1;）  
    完成
- FEAT: 首次启动时应该显示启动画面附带使用说明  
    完成。改成制作开场。
- TODO: 测试视频结束后再开始是否工作正常  
    完成。

________________________________________
##### 当前任务

________________________________________
##### 计划任务

- TODO: 列举出\[\]问题的多种重现方法。（使用assert()检查？）
- TODO: 关键方法有安全性问题。看影响程度与站方开发协商扩展API：点击输入框填入自动建议内容。

      Player.commentTrigger(onComment:Function, timeout_msec:Number = 1000, suggest:Boolean = false)
          if (suggest) {
              var getSuggestion = onComment;
              //commentTriggerManager...?
              normalCommentInput.textInput.addEventListener('click', function(e) {
                  if (normalCommentInput.textInput.text === '') {
                      normalCommentInput.textInput.text = getSuggestion();
                      normalCommentInput.textInput.text.selectAll();//用户可以直接忽略建议，开始输入
                  }
              });
          }
- FEAT: 数据分片重组传输克服字数限制，需要UI合理设计  
    下一版实现。
- FEAT: 减少$.root依赖
- FEAT: 重构，使用.cacheAsBitmap = true
- FEAT: 重构，使用MotionManager进行调度
- BUG: 初始化后未显示已经处理的涂鸦弹幕  
    细节，以后修复。
