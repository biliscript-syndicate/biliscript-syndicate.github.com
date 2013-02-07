---
layout: post
title : 沙发
tagline : 日志模式
author : nekofs
description : ""
category : 
tags : []
---
{% include JB/setup %}

Does split filter work?

{% assign testArray = "a+b+c+d+e+f" | split:"+" %} 
{% for item in testArray %} 
{% comment %} 
adding this condition as split adds the separator to the splitted array 
{% endcomment %} 
{% if item != "+" %} 
{{item}}- 
{% endif %} 
{% endfor %} 

Test b:

{% assign a = '1,2,3,4' | split:"," %}
{{ a[1] }}
