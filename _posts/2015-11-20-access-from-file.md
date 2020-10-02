---
layout: post
title:  浏览器打开本地文件资源的设置
date:   2015-11-20 10:45:43
categories: webgl
---

转自：[http://www.cnblogs.com/twaver/p/3710941.html](http://www.cnblogs.com/twaver/p/3710941.html)

随着mono-design不断推广，用户越来越多，陆续有电话来询问“为什么3D展现的时候，是一团黑？”，针对这个问题，专门写个帖子说明原因并给出解决方案，并且在mono-design编辑器中加了判断功能，同时链接到这里，不用等到发现一团黑时，才知道出问题。

好了，言归正传，开始分析问题：
当发现3D展现是一团黑的时候，在控制台如果看到“Unable to get image data from canvas because the canvas has been tainted by cross-origin data.”的错误提示，这是因为浏览器的安全策略，“同源策略”。浏览器为了阻止欺骗，会追踪 image data。当你把一个“跟canvas的域不同的”图片放到canvas上，这个canvas就成为 “tainted”(被污染的，脏的)，浏览器就不让你操作该canvas 的任何像素。

这个问题有两种解决方案

方案一：有服务器环境，将项目部署在web服务器上，最简单的tomcat。
mono-design的目录中并直接移动到例如apache-tomcat-6.0.37\webapps\ROOT\下，然后浏览器打开后输入http://localhost/mono-design/即可。

方案二：设置浏览器
On Windows：

Chrome:
1. 得到Chrome的安装路径，例如：
C:\Users\-your-user-name\AppData\Local\Google\Chrome\Application
2. 在命令行窗口，输入安装路径，加上–allow-file-access-from-files参数，例如：
Chrome installation path\chrome.exe --allow-file-access-from-files
，回车执行，启动Chrome
3. 测试的一个临时方法:：复制一个Chrome的快捷方式，右键->属性->目标的文本框中加上参数
--allow-file-access-from-files
，例如：
"Chrome installation path\chrome.exe" --allow-file-access-from-files
IE11：默认可以加载本地图片

Firefox：
1. Firefox的用户请在浏览器的地址栏输入“about:config”，回车
2. 在过滤器（filter）中搜索“security.fileuri.strict_origin_policy”
3. 将security.fileuri.strict_origin_policy设置为false
4. 关闭目前开启的所有Firefox窗口，然后重新启动Firefox。

On Mac：

Chrome：从命令行窗口中启动，启动命令为

open /Applications/Google\ Chrome.app --args --allow-file-access-from-files
Safari：
1. Safari->偏好设置->高级->勾选“在菜单栏中显示‘开发’菜单”
2. 开发->勾选“启用WebGL”
3. 开发->勾选“停用本地文件限制”

Firefox：
1. Firefox的用户请在浏览器的地址栏输入“about:config”，回车
2. 在过滤器（filter）中搜索“security.fileuri.strict_origin_policy”
3. 将security.fileuri.strict_origin_policy设置为false
4. 关闭目前开启的所有Firefox窗口，然后重新启动Firefox。

