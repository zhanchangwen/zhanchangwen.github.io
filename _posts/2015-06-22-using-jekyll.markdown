---
layout: post
title: "Using Jekyll"
date:   2015-06-22 13:46:54
categories: jekyll update
---
安装过程：

1.下载安装[ruby][ruby-installer]

2.下载[devkit][ruby-devkit]并解压

cd <devkit directory>

ruby dk.rb init

编辑config.yml 最后一行改为  - <ruby directory>;如： - C:\Ruby200-x64

ruby dk.rb installer

3.安装jekyll

gem install jekyll

4.软件管家安装python

将python安装路径、安装路径\Scripts添加到path环境变量中

5.安装Pygments

easy_install pygments

6.使用jekyll

cd 制定目录

jekyll new blog

_config.yml中添加 hightlight:pygments

cd blog

jekyll serve

在浏览器中浏览http://localhost:4000

在安装配置jekyll过程中碰到的问题：

easy_install jekyll  失败

使用git bash，不要用dos命令行

[ruby-installer]: http://dl.bintray.com/oneclick/rubyinstaller/ruby-2.2.2-x64-mingw32.7z
[ruby-devkit]:    http://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe