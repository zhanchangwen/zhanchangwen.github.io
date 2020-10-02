---
layout: post
title:  安装配置Spring
date:   2015-10-24 10:57:44   
categories: technique
---
[http://blog.csdn.net/hanshileiai/article/details/37882135](http://blog.csdn.net/hanshileiai/article/details/37882135 "Spring 的下载、安装和使用")

一、下载 Spring 下载地址：http://repo.spring.io/libs-release-local/org/springframework/spring/4.0.6.RELEASE/    下载zip压缩包:  spring-framework-4.0.6.RELEASE-dist.zip 并解压。
 

二、在 Eclipse 呀 myEclipse 中开发 Spring 应用
 

  1. 新建 java project  项目命名为 myspring
  2. 为该项目增加 Spring 支持。添加用户库 spring4.0.6 和 common-logging 添加方法如下图：


commons-logging-1.1.3.jar



  3. 定义一个 Spring 管理容器中的 Bean  (POJO)  src\hsl\service\PersonService.java 代码如下： 
[java] view plaincopy在CODE上查看代码片派生到我的代码片
package hsl.service;  
  
public class PersonService {  
    private String name;  
  
    // name属性的setter方法  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    // 测试Person类的info方法  
    public void info() {  
        System.out.println("此人名为：" + name);  
    }  
}  
注：Spring 可以管理任意的 POJO，并不要求 java 类是一个标准的 JavaBean.

  4. 编写主程序，该程序初始化 Spring 容器 src\hsl\SpringTest.java  代码如下：
[java] view plaincopy在CODE上查看代码片派生到我的代码片
package hsl;  
  
import hsl.service.PersonService;  
import org.springframework.context.ApplicationContext;  
import org.springframework.context.support.ClassPathXmlApplicationContext;  
  
public class SpringTest {  
    public static void main(String[] args) {  
        // 创建Spring的ApplicationContext  
        ApplicationContext ctx = new ClassPathXmlApplicationContext("bean.xml");  
        System.out.println(ctx); // 输出Spring容器  
  
        // 通过 Spring 容器获取 Person 实例，并为 Person 实例设置属性值（这种方式称为控制反转，IoC）  
        PersonService p = ctx.getBean("personService", PersonService.class);  
        p.info();  
    }  
}  
  5. 将 PersionService 类部署在 Spring 配置文件中， src\bean.xml  代码如下：
[html] view plaincopy在CODE上查看代码片派生到我的代码片
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xmlns="http://www.springframework.org/schema/beans"  
    xsi:schemaLocation="http://www.springframework.org/schema/beans  
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">  
    <!-- 将PersonService类部署成Spring容器中的Bean  -->  
    <bean id="personService" class="hsl.service.PersonService">  
        <property name="name" value="wawa"/>  
    </bean>  
</beans>  
  6. 运行主程序，结果如下：

 