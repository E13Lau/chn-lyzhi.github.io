---
layout: post
title:  "iOS 开发-UIScrollView + Auto Layout + Size Classes"
date:   2015-07-13 14:35
categories: jekyll update
tags: iOS
---

* Storyboard 中把 ViewController 的 top Bar 设为 `Opaque Navigation Bar`
* 拖拽一个 ScrollView 到 ViewController 中
* 添加 ScrollView 的约束，注意去掉 margin 的勾勾，这是边缘
* 拖拽一个需要动态变动高度的 Label 到 ScrollView 中
* 设置 Label 属性，Lines 设为0，添加需要的约束，并把 `Intrinsic Size` 设为 `Placeholder`
* 注意添加一个固定高度（可为0）、与 ScrollView 同宽的 View

-------------------------------

Tips:

* AutoLayout + SizeClasses 的思想是把 View 的大小、位置抽象化，所以在 Storyboard 中一个 Label 是这样，但是实际却是这样（图）
* ScrollView 中只有动态控件，ScrollView 的 ContentSize 无法确定，添加一个 View，并设置 View 与 ScrollView `Equal Width`，想要隐藏就设置高度为0，并勾选固定高度
* ScrollView 作为 View Controller 的首个 View 时，ScrollView 的 `Top Alignment Constraint` 约束中 First item 为 `Scroll View.Top`，Second Item 为 `Top Layout Guide.Top`。当Second Item 为 `Top Layout Guide.Bottom` 时 ScrollView 的 bounds.y 被定为64。Like this（图）

Question:

* 当 ScrollView 的 `Top Alignment Constraint` 的 `Second Item` 值为 `Top Layout Guide.Bottom` 时， ScrollView 的 bounds 的 y 值被加64，且 Navgation 没有透明效果，当 `Second Item` 的值为 `Top Layout Guide.Top` 时，反而相反。
* ScrollView 作为 Controll 的第一个View，contentSize 不起作用？

-----------------

利用自动布局自动排列 n 个高宽相等，间距相等，水平或垂直对其的 View。

* 选中第一个 View，设置上、左约束（根据需要）
* 选中最后一个 View，设置上、右约束（根据需要）
* 全选 View，添加高度固定数值、等宽、顶部对齐
* 两两添加 水平间隔，并把每一条水平间隔设为0
* 更新所有 Frame

![Gif](/assets/AutoLayout三等分.gif)