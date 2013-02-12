---
layout: page
title: "性能"
description: ""
category: 
tags: []
---
{% include JB/setup %}

60帧每秒，16000微秒每帧。

    function perf(name, exec) {
        var N = 100000, i;
        var idle = function(){};
        var start = getTimer();
        i = N; while (i--) idle();
        var idleRate = (getTimer() - start) * 1000 / N;
        start = getTimer();
        i = N; while (i--) exec();
        var rate = (getTimer() - start) * 1000 / N;
        trace(name, Math.round((rate - idleRate) * 1000) / 1000, 'us/op');
    }

### 循环方法

while循环最好。

    N = 10000000;
    start = getTimer();
    for (var i = 0; i < N; i++);
    trace('for-loop', (getTimer() - start) * 1000 / N, 'us/op');

    start = getTimer();
    for (var i = N; i--;);
    trace('for-loop2', (getTimer() - start) * 1000 / N, 'us/op');

    start = getTimer();
    var i = N;
    while (i--);
    trace('while-loop', (getTimer() - start) * 1000 / N, 'us/op');

    //for-loop 1.2013 us/op
    //for-loop2 0.7189 us/op
    //while-loop 0.6223 us/op

### Utils.rgb()

手动比Utils.rgb()快一倍。主要时间花在函数调用。

    rgb = Utils.rgb;
    r, g, b, result;

    perf('manual', function() { r << 16 | g << 8 | b; });
    perf('Utils.rgb()', function() { rgb(r, g, b); });

    //manual 1.488 us/op
    //Utils.rgb() 2.998 us/op

### 数组访问方法

Array.\[\]略快于Vector.\[\]。（.forEach()和foreach()慢较多，结果未写在这里，时间花在函数调用。）

    a = [1];
    v = $.toIntVector(a);

    perf('Array.[]', function(){ a[0]; });
    perf('Vector.[]', function(){ v[0]; });

    //Array.[0] 0.676 us/op
    //Vector.[] 0.797 us/op

