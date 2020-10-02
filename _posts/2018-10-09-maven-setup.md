
---
layout: post
title: "maven setup"
date:   2018-10-9 21:16:52
categories: maven
---

##安装方式
1. 下载maven包，并解压[maven官方网站](http://maven.apache.org/download.cgi)
2. 配置环境变量M2_HOME={MAVEN_DIR}
3. 配置环境变量PATH=%M2_HOME%\bin;注意不同操作平台配置环境变量之间的差异

##常用链接
1. [maven中央仓库](http://repo.maven.apache.org/maven2/)
2. [maven插件介绍](

###由于无法翻墙，需要配置第三方仓库
* 方法一：{MAVEN_DIR}/conf/settings.xml对应标签增加以下内容

```linux
<mirror>  
  <id>alimaven</id>  
  <name>aliyun maven</name>  
  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>;  
  <mirrorOf>central</mirrorOf>          
</mirror>
```
* 方法二：在项目的pom.xml加入

```linux
<repositories>  
    <repository>  
        <id>maven-ali</id>  
        <url>http://maven.aliyun.com/nexus/content/groups/public//</url>;  
        <releases>  
            <enabled>true</enabled>  
        </releases>  
        <snapshots>  
            <enabled>true</enabled>  
            <updatePolicy>always</updatePolicy>  
            <checksumPolicy>fail</checksumPolicy>  
        </snapshots>  
    </repository>  
</repositories>
```


###maven目录架构
* app
    * src
        * main
            * java
            * resource
        * test
            * java
            * resource
    * pom.xml #maven的配置文档

* 查看插件使用说明

```linux
 mvn help:describe -Dplugin=org.apache.maven.plugins:maven-archetype-plugin
```
### 使用模板创建maven项目

```linux
 mvn archetype:create -DarchetypeCatalog=internal
 #由于maven提供的模板数量太多，所以使用-DarchetypeCatalog=internal，显示精简的模板
```
### 将创建的maven项目转换为eclipse项目

```linux
 mvn eclipse:eclipse
 #执行该命令，会对当前项目生成eclipse所需要的.classpath和.project文件
 #修改pom.xml增加新的依赖时，也可使用该命令下载依赖包
```

* 编译

```linux
 mvn compiler:compile
 #此时会新增target目录，里面包含针对src/main目录下的java文件生成的class文件
```
* 编译测试程序

```linux
 mvn compiler:testCompile
 #此时会新增target目录，里面包含针对src/test目录下的java文件生成的class文件
```
* 执行单元测试

```linux
 mvn surefire:test
 #此时会新增target目录，里面包含针对src/test目录下的java文件生成的class文件
```
* 清理mvn产生的文件

```linux
 mvn clean
```
* 将项目进行打包

```linux
 #依赖maven插件shade，将依赖包一起打包
 mvn package
 #此为生命周期阶段命令，可理解为编译、测试、打包的合集
```

###常用生命周期命令

```linux
 mvn compile
 mvn test
 mvn package
```

### 教程推荐
[网易云课堂：maven](https://study.163.com/course/courseMain.htm?courseId=1003456010)

### 操作源码
