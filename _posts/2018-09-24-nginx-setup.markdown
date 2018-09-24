---
layout: post
title: "nginx setup on CentOS"
date:   2018-9-24 14:42:16
categories: nginx
---

1.安装依赖包
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
2.安装 PCRE,让 Nginx 支持 Rewrite 功能
http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
3.安装nginx
http://nginx.org/download/nginx-1.6.2.tar.gz
4.启动
nginx/sbin/nginx 