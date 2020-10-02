---
layout: post
title:  JAVA环境搭建
date:   2013-09-3 13:46:54
categories: technology
---

# 1.下载安装jdk #

windows下jdk下载：(点击直接下载或者右键复制链接地址)
	
[jdk1.7 32bit](http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-windows-i586.exe)

[jdk1.7 64bit](http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-windows-x64.exe)

[jdk1.8 32bit](http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-windows-i586.exe)

[jdk1.8 64bit](http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-windows-x64.exe)


# 2.设置环境变量 #

JAVA_HOME

jdk的安装路径。如：C:/Program Files/Java/jdk1.7.0

path

%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

CLASS_PATH

.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;


# 3.测试是否安装成功 #

打开命令行 win+R --> cmd

输入javac，查看是否打印信息

参考：[百度经验](http://jingyan.baidu.com/article/f96699bb8b38e0894e3c1bef.html)