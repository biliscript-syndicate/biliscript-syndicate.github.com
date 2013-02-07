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

Test c:

{% capture data %}
1 2 3
4 5 6
7 8 9
{% endcapture %}
{{ data | newline_to_br }}
{% assign array = data | newline_to_br | split: '<br />' %}
{% for item in array %}
{{item}},
{% endfor %}
