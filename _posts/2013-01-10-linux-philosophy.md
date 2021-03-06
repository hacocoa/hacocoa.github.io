---
layout: post
title: Linux哲学
date: 2013-01-10 00:05
comments: true
categories: [back-end]
---

因为在研究一个开源项目[fontello](https://github.com/fontello/fontello)，它是一个可以把很多开源字体聚合在一起，访客可以自由打包，选择自己项目需要的图标，最终下载一个完整的字体包，还有对应的CSS和demo页。

我非常感兴趣的一点是这个开源项目本身使用了大量开源项目（包括开源字体和开源工具）作为子模块。我以前不了解Linux编程，但觉得这种集各家之长来完成一个大项目的工作流程很赞。

所以我翻了一下[《GNU Make项目管理》]()这本书，了解了下makefile的基本语法，然后了解到，我如果希望写出能用的makefile文件，需要熟悉shell语法，然后我就看了*Linux Shell Scripting Tutorial*这本书。里面有一节提到*Linux哲学*。

* *一个程序只做一件事，并做好。*程序要能协作。程序要能处理文本流，因为这是最通用的接口。
* *一切皆是文件。*设备也是文件。
* *小的就是美的。*
* *在文本文件中存储配置和数据。*因为文本是通用接口，它容易创建，备份和移动到其他系统。
* *使用shell命令来增加杠杆性和可移植性。*
* *把不同的程序链接在一起完成复杂任务。*
* *可移植性高于效率。*
* *简单，直观。（KISS）*

这是非常简单的一个列表，如果感兴趣，还可以看看这篇[unix哲学](http://www.linuxsong.org/2010/09/unix-philosophy/)。继续学习shell。