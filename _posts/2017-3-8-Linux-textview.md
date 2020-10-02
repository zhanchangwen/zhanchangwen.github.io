---
layout: post
title:  文本查看命令
date:   2017-3-8 12:11:23
categories: Linux
---
##常用参数
	-A, --show-all 等价于 -vET
	-b, --number-nonblank 对非空输出行编号
	-e 等价于 -vE
	-E, --show-ends 在每行结束处显示 $
	-n, --number 对输出的所有行编号
	-s, --squeeze-blank 不输出多行空行
	-t 与 -vT 等价
	-T, --show-tabs 将跳 字符显示为 ^I


##编辑并编辑文件
	cat >  linuxsir.org.txt  << EOF
	追加使用 >>
##多个文件输出到一个文件
	cat sir01.txt sir02.txt sir03.txt >> sir00.txt
##清空文件
	cat /dev/null > test.txt
