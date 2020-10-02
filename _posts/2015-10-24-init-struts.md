---
layout: post
title:  安装配置struts2
date:   2015-10-24 10:06:01  
categories: technique
---
[http://www.cnblogs.com/netshuai/archive/2009/07/23/1529700.html](http://www.cnblogs.com/netshuai/archive/2009/07/23/1529700.html "struts2框架安装及配置")

1、打开http://struts.apache.org/网站，点击右上角的struts2，在进入的页面点击Download Now，下载Full Distribution（完整版），并解压。
2、复制lib目录下的commons-logging-1.0.4.jar，freemarker-2.3.13.jar，ognl-2.6.11.jar，struts2-core-2.1.6.jar，xwork-2.1.2.jar到/WEB-INF/lib目录下（其他jar文件请根据需要复制）。
另：commons-fileupload-1.2.1.jar，commons-io-1.3.2.jar两个包有时不导入会出问题。
3、在/WEB-INF/下的web.xml中添加
 

复制代码
     <filter>
      <filter-name>struts2</filter-name>
      <filter-class>
       org.apache.struts2.dispatcher.FilterDispatcher
      </filter-class>
     </filter>
    
     <filter-mapping>
      <filter-name>struts2</filter-name>
      <url-pattern>/*</url-pattern>
     </filter-mapping>
复制代码

4、在src目录中新建struts.xml文件，内容示例如下：

    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE struts PUBLIC
        "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
        "http://struts.apache.org/dtds/struts-2.0.dtd">
    
    <struts>
    
     <package name="struts2" extends="struts-default">
    
      <action name="login" class="com.test.action.LoginAction">
       <result name="input">/login2.jsp</result>
       <result name="success">/result.jsp</result>
      </action>
     
    
     </package>
    
    </struts>
