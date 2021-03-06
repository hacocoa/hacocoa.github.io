---
layout: post
title: 匹配项目的栅格化系统
date: 2011-01-07 00:39
comments: true
categories: [front-end]
---
<h2>一个前提</h2>
当我们说<a href="http://960.gs">960gs</a>或者<a href="http://www.webdesignerwall.com/trends/960-grid-system-is-getting-old/">978gs</a>的时候，这个数字代表的是什么？要知道在栅格系统中栅格总宽度和可视宽度是不相等的，前者比后者打一个gutter的宽度。在960gs中，960是指栅格总宽度，在978gs中，978是指可视宽度。这一点小小的区别没有打成共识，可能会浪费大量的会议时间来争吵，主持人却不知道大家卡在哪里了。
<h2>960是神圣的吗？</h2>
我的回答是否。

在讨论中我听见非HTML/CSS专业人士一直在提出的一个问题是，那么多人用960像素宽一定是有道理的，那我们为什么非要用992呢？对此我的回答分两个部分，首先说明为什么960是广受欢迎的，其次说明为什么这个数字不适合我们的项目。
<h3>为什么960广受欢迎？</h3>
因为960是一个神奇数字，能被很多偶数整除，包括12、16、24等，而且除出来的数字都是10的倍数。因为这个数字很能除，所以它被应用在一个有名的栅格系统叫“960栅格系统”上，这个系统能匹配上12栏布局、16栏布局，24栏布局的各种设计稿。也正是因为这个原因，它被大量的希望快速开发的设计师/开发者广泛使用了。

这里值得说明的一点是，要在主流浏览器和分辨率上完整显示而不出现水平滚动条的最大宽度是<a href="http://yuguo.us/997/">997像素</a>，而960是小于997像素的一个最大神奇数字。因为1920肯定也是神奇数字，不过在这个时代还没有那么多人有大屏幕显示器。
<h3>为什么这个数字不适合我们的项目？</h3>
因为960栅格系统意味着可视区域肯定没有960像素——如果gutter是20像素，那么可视940；如果gutter10像素，那么可视950，<em>无论哪种都是产品经理和设计师无法接受的</em>。网站是一个有较多图片的娱乐站点，希望给用户大气上流的感觉，就不能太窄。这是第一个原因。

第二个原因是，960是普遍适用的，但我们寻找的数字<em>不需要是普遍适用</em>的，它需要符合项目就好了，项目能确定16栏，我们就不要求这个数字是24的倍数。
<h2>我的建议是使用自己计算出的992栅格。</h2>
16栏，每栏42像素，gutter20像素，实际可视区域972像素。

