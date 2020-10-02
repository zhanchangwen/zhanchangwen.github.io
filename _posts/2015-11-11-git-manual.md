---
layout: post
title:  git教程-远程仓库的基本使用
date:   2015-11-06 10:06:14  
categories: git
---
 
参考：[廖雪峰官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

将远程仓库添加到本地
	$ git remote add origin git@github.com:michaelliao/learngit.git

将本地库的所有内容推送到远程库
	$ git push -u origin master

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；