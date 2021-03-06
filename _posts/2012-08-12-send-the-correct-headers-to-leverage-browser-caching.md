---
layout: post
title: 如何正确设置缓存
date: 2012-08-12 18:57
comments: true
categories: [front-end]
---

web页面变得越来越胖，这意味着更多脚本、样式、图片和flash。初次访问站点的访客不得不请求很多HTTP请求，但是可以通过设置Expire头来让这些文件缓存起来，避免重复的HTTP请求。Expire头经常用在图片上，但在脚本、样式和flash上都应使用这一技术。
<h2>Expire</h2>
Expire头的设置在服务器端进行，服务请求通过在HTTP相应中增加Expire头来告诉客户端该文件可以缓存多久，比如：
<pre>Expires: Thu, 15 Apr 2020 20:00:00 GMT</pre>
告诉浏览器，该文件在2020年之前都不会过期。

比如<a href="http://33pu.net/">33号铺</a>的样式返回的Expires：
<a href="http://yuguo.us/files/2012/08/1.png"><img class="aligncenter size-full wp-image-1348" title="1" src="http://yuguo.us/files/2012/08/1.png" alt=""   /></a>
所以浏览器再次访问这个资源的时候，可能是输入地址访问，我们可以看到：
<a href="http://yuguo.us/files/2012/08/2.png"><img class="aligncenter size-full wp-image-1349" title="2" src="http://yuguo.us/files/2012/08/2.png" alt=""   /></a>
如果我F5，会看到下图（304下面解释）
<a href="http://yuguo.us/files/2012/08/12.png"><img class="aligncenter size-full wp-image-1363" title="1" src="http://yuguo.us/files/2012/08/12.png" alt=""   /></a>
最好如果我Ctrl+F5，就会看到下图：
<a href="http://yuguo.us/files/2012/08/3.png"><img class="aligncenter size-full wp-image-1350" title="3" src="http://yuguo.us/files/2012/08/3.png" alt=""   /></a>
如果你的服务器是Apache，可以通过ExpiresDefault来配置一个相对现在日期的时间段。比如：
<pre>ExpiresDefault "access plus 10 years"</pre>
时刻记住，如果你使用了超长缓存，那么希望变更文件的时候就必须使用另一个文件名了。在Qzone我们使用时间戳来实现修改文件名的效果：
<pre><a href="http://qzonestyle.gtimg.cn/qzone_v6/icenter.css?max_age=31536000&amp;d=2012524161750">http://qzonestyle.gtimg.cn/qzone_v6/icenter.css?max_age=31536000&amp;d=2012524161750</a></pre>
这个url中?后面的字符只要跟客户端缓存中的字符不匹配，客户端就会认为是新的图片。值得说明的是，Qzone使用HTTP 304而不是Expire来实现缓存控制。
<h2>HTTP 304（Cache-control）</h2>
304 的标准解释是：Not Modified 客户端有缓冲的文档并发出了一个条件性的请求（一般是提供If-Modified-Since头表示客户只想比指定日期更新的文档）。服务器告诉客户，原来缓冲的文档还可以继续使用。

如果客户端在请求一个文件的时候，发现自己缓存的文件有 Last Modified ，那么在请求中会包含 If Modified Since ，这个时间就是缓存文件的 Last Modified 。因此，如果请求中包含 If Modified Since，就说明已经有缓存在客户端。只要判断这个时间和当前请求的文件的修改时间就可以确定是返回 304 还是 200 。对于静态文件，例如：CSS、图片，服务器会自动完成 Last Modified 和 If Modified Since 的比较，完成缓存或者更新。但是对于动态页面，就是动态产生的页面，往往没有包含 Last Modified 信息，这样浏览器、网关等都不会做缓存，也就是在每次请求的时候都完成一个 200 的请求。

所以第一次请求：
<a href="http://yuguo.us/files/2012/08/11.png"><img class="aligncenter size-full wp-image-1351" title="1" src="http://yuguo.us/files/2012/08/11.png" alt=""   /></a>
对于第二次请求：
<a href="http://yuguo.us/files/2012/08/21.png"><img class="aligncenter size-full wp-image-1352" title="2" src="http://yuguo.us/files/2012/08/21.png" alt=""   /></a>
注意看清楚Request和Response的区别。

跟Expire一样的是：

第一次访问 200

鼠标点击二次访问 (Cache)

按F5刷新 304

按Ctrl+F5强制刷新 200
<h2>Expires vs Cache-control</h2>
200(缓存)是最快的，因为没有请求发生。304则产生了HTTP请求：浏览器发送一个带有If-Modified-Since的请求，服务器根据情况返回304来告诉浏览器使用本地文件。

所以304比200（缓存）慢一点，静态文件都应该使用Expires头来减少请求，提高访问速度。（根据HTTPWATCH的说法：“Don't cache HTML, Cache everything else forever”）

如果服务器又设置了Cache-Control:max-age和Expires呢，怎么办？
<strong>答案是同时使用</strong>，也就是说在完全匹配If-Modified-Since和If-None-Match即检查完修改时间和Etag之后，服务器才能返回304.(不要陷入到底使用谁的问题怪圈)

参考资料：<a href="http://blog.httpwatch.com/2007/12/10/two-simple-rules-for-http-caching/">http://blog.httpwatch.com/2007/12/10/two-simple-rules-for-http-caching/</a><a href="http://developer.yahoo.com/performance/rules.html#expires">http://developer.yahoo.com/performance/rules.html#expires</a><a href="http://www.ardamis.com/2010/07/17/sending-headers-to-leverage-browser-caching/">http://www.ardamis.com/2010/07/17/sending-headers-to-leverage-browser-caching/</a><a href="http://stackoverflow.com/questions/535053/which-webbrowsers-use-http-1-1-by-default">http://stackoverflow.com/questions/535053/which-webbrowsers-use-http-1-1-by-default</a>
