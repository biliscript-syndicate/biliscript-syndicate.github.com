---
layout: page
title: "convertHSBtoRGB()"
category: examples
---
{% include JB/setup %}

最小色调0 ![色谱](data:image/png;base64,
iVBORw0KGgoAAAANSUhEUgAAAWgAAAAICAIAAABbBPJsAAAAY0lEQVR42u3UQQqAIBAF0Cnq/gdW
qE1gYFBCpYv3mMU4iDAgf9oiYjnV2t6X5r8+ReSj3us/ebBUtUw5jjtP18uMO8+3G9bb9r/f+BNz
9/tzADQSHIDgAAQHIDgAwQEIDoAndlMAtBP+rF7lAAAAAElFTkSuQmCC) 最大色调360（开区间）。

    ////////////////////////////////////////////////////////////////////////////////
    //
    //  ADOBE SYSTEMS INCORPORATED
    //  Copyright 2008 Adobe Systems Incorporated
    //  All Rights Reserved.
    //
    //  NOTICE: Adobe permits you to use, modify, and distribute this file
    //  in accordance with the terms of the license agreement accompanying it.
    //
    ////////////////////////////////////////////////////////////////////////////////

    function convertHSBtoRGB(hue, saturation, brightness) {
        // Conversion taken from Foley, van Dam, et al
        var r, g, b;
        if (saturation == 0) {
            r = g = b = 1;
        } else {
            var h = (hue % 360) / 60;
            var i = h | 0;
            var f = h - i;
            var p = 1 - saturation;
            var q = 1 - saturation * f;
            var t = 1 - saturation * (1 - f);
            switch (i) {
                case 0: r = 1; g = t; b = p; break;
                case 1: r = q; g = 1; b = p; break;
                case 2: r = p; g = 1; b = t; break;
                case 3: r = p; g = q; b = 1; break;
                case 4: r = t; g = p; b = 1; break;
                case 5: r = 1; g = p; b = q; break;
            }
        }
        r *= 255 * brightness;
        g *= 255 * brightness;
        b *= 255 * brightness;
        return r << 16 | g << 8 | b;
    }

TODO: 补充测试用例
