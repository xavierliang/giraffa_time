---
layout: post
title: "网页上的中文字体"
date: 2015-03-22 18:00:00
categories: 前端
author: xavier
---

如何选择字体是网页开发中非常重要的因素之一，它会影响到美观、阅读体验。

英文字体非常方便，因为系统自带字体较多，且字体文件小，在线加载也没有任何问题。

可中文网站则完全不同，不同的操作系统、设备中的自带字体千差万别，而且中文字体文件最少也有几个MB，所以只能依靠系统中预装的中文字体。

#### Font-Family使用方法

Font-Family的渲染规则：

    1. 优先使用排在前面的字体；

    2. 如果找不到该字体，或者该字体不包括所要渲染的文字，则使用下一种字体；

    3. 如果所列出的所有字体都无法满足需要，则让操作系统自行决定使用哪种字体。

所以英文字体应该排在前面：

{% highlight css %}
font-family: Georgia, "Times New Roman", "Hiragino Sans GB", "冬青黑体", SimHei, "黑体";
{% endhighlight %}

其中，带空格的英文名称，以及中文名称，都应该放在双引号内。

另外，为了保证兼容性，中文字体的中文名称和英文名称都应该写入font-family。

#### 预装字体

##### Windows

    - 黑体：SimHei
    
    - 宋体：SimSun

    - 新宋体：NSimSun

    - 仿宋：FangSong

    - 楷体：KaiTi

    - 微软雅黑：Microsoft YaHei

##### OS X

    - 冬青黑体：Hiragino Sans GB

    - 华文细黑：STHeiti Light

    - 华文黑体：STHeiti

    - 华文楷体：STKaiti

    - 华文宋体：STSong

    - 华文仿宋：STFangsong

由于不同操作系统中的中文字体几乎没有交集，所以应该分别为两个平台指定字体。
