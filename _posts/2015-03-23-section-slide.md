---
layout: post
title: 移动端的PPT
date: 2015-03-23 18:00:00+0800
author: xavier
categories: 前端
---

随着智能手机的使用越来越普及，针对手机端的业务介绍、邀请函越来越多。

不过使用第三方提供的编辑器却存在各种问题，比如过于花哨、动画效果不满意、有广告。于是闲暇时间做了一个简单的库，提供js与css的支持，用户只需要简单写点html就可以满足上面的需求。

[源码](https://github.com/xavierliang/sectionSlide)

#### 手机上的PPT

设计思路源于PPT，有层次、有结构地展现要表达的内容即可。

考虑到手机上的交互应该简单明了，所以只需要涉及上下或者左右滑动两个动作。而滑动过程中可选择不同的动画或者切换效果。

#### 如何使用

%section.scene 表示一个页面。

%section.slide 表示页面内的一个slide，一个页面中可以有多个slide，slide在滑动过程中在该页面内变动。

.fragment 为 %section.slide 内的元素，如果设定参数 data-auto 不为零，则自动播放，单位为毫秒。

css模板中默认提供的动画效果如下：

    .fix    //固定效果
    .fade   //渐变
    .up     //向上滑动
    .left   //向左滑动
    .cube   //方块滚动
    .shrink //缩放
    .roll   //滚动

使用方式如下(haml)：

    %section.scene
        %section.slide
        %section.slide
            .fragment(data-auto=500 data-exempt=5)
            .fragment(data-auto=500)
            .fragment(data-clear=3)
    %section.scene
        %section.slide

#### 例子

    %section.scene.fix.up_after
        %h1 这是第一页
    %section.scene.up.up_after
        %h1.title 这是第二页
        %section.slide.fade.fix.cube_after
            %p 第一个slide
            %p 内容
        %section.slide.fade.cube.cube_after
            %p 第二个slide
            %p 内容
        %section.slide.fade.cube.cube_after
            %p 第三个slide
            %p 内容
    %section.scene.up.left_after
        %h1
        %section.slide.fade.fix.cube_after
        ...
    %section.scene.left.left_after
        %h1
        ...

#### fragment data 参数

    data-auto 自动播放的时间，单位为毫秒。若该参数为零或者不填，则手动播放
    data-clear 表示清楚之前出现的 data-exempt 小于data-clear 的 fragment，若之前的某个 fragment 的 data-exempt 大于或等于 data-clear，则不被清楚。

[源码](https://github.com/xavierliang/sectionSlide)
