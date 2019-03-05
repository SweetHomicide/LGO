---
layout:     post
title:      Idea maven 构建项目多模块开发手册
subtitle:   Idea maven 构建项目多模块开发手册
date:       2018-12-05
author:     V
header-img: img/homicide/home-bg.jpg
catalog: true
tags:
    - Maven
    - Springboot
    - 多模块开发
---

# Idea maven 构建项目多模块开发手册

### 构建maven顶级项目
  
> step 1 

![](https://i.imgur.com/VUSsrmw.png)  

> 2   
   
![](https://i.imgur.com/PuIYJAx.png)

> 3    
   
![](https://i.imgur.com/J2pH8iZ.png)

> 4  
   
![](https://i.imgur.com/JsvAsYn.png)


### 在顶级项目中构建多模块

> 1   
 
![](https://i.imgur.com/4Qgh1WQ.png)   

> 2  

![](https://i.imgur.com/c1fr1c9.png)  
 
> 3  
  
![](https://i.imgur.com/3wmN8HW.png)  

> 4  
  
![](https://i.imgur.com/c9A0dnT.png)  

> 5 
  
![](https://i.imgur.com/p8SdheW.png)

> 6 
  
![](https://i.imgur.com/aZmnmj2.png)

> 7 聚合工程pom
	  
	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	  <modelVersion>4.0.0</modelVersion>
	  <groupId>pub.lgo</groupId>
	  <artifactId>TAOZUI</artifactId>
	  <version>1.0-SNAPSHOT</version>
	  <packaging>pom</packaging>
	
	  <name>TAOZUI</name>
	  <!-- FIXME change it to the project's website -->
	  <url>http://www.example.com</url>
	
	  <properties>
	    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	    <maven.compiler.source>1.7</maven.compiler.source>
	    <maven.compiler.target>1.7</maven.compiler.target>
	  </properties>
	
	  <!-- 多模块开发需要使用该标签聚合子模块；在子模块中需要继承顶级项目的pom文件 -->
	  <modules>
	    <module>tz-font</module>
	    <module>tz-login</module>
	  </modules>
	  <!-- 解决单依赖问题.子模块需要继承spring-boot-starter-parent 而在子模块中已经继承了该聚合pom作为依赖
	    在此引用springboot给出的解决方案使用spring-boot-dependencies作为依赖;
	    详见：https://docs.spring.io/spring-boot/docs/1.4.3.RELEASE/reference/htmlsingle/#using-boot-maven-without-a-parent
	    此种方式必须在dependencyManagement标签内有效-->
	  <dependencyManagement>
	    <dependencies>
	      <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-dependencies -->
	      <dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-dependencies</artifactId>
	        <version>2.1.3.RELEASE</version>
	        <type>pom</type>
	        <scope>import</scope>
	      </dependency>
	    </dependencies>
	  </dependencyManagement>
	
	  <dependencies>
	    <dependency>
	      <groupId>junit</groupId>
	      <artifactId>junit</artifactId>
	      <version>4.11</version>
	      <scope>test</scope>
	    </dependency>
	  </dependencies>
	
	  <build>
	    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
	      <plugins>
	        <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
	        <plugin>
	          <artifactId>maven-clean-plugin</artifactId>
	          <version>3.1.0</version>
	        </plugin>
	        <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
	        <plugin>
	          <artifactId>maven-resources-plugin</artifactId>
	          <version>3.0.2</version>
	        </plugin>
	        <plugin>
	          <artifactId>maven-compiler-plugin</artifactId>
	          <version>3.8.0</version>
	        </plugin>
	        <plugin>
	          <artifactId>maven-surefire-plugin</artifactId>
	          <version>2.22.1</version>
	        </plugin>
	        <plugin>
	          <artifactId>maven-jar-plugin</artifactId>
	          <version>3.0.2</version>
	        </plugin>
	        <plugin>
	          <artifactId>maven-install-plugin</artifactId>
	          <version>2.5.2</version>
	        </plugin>
	        <plugin>
	          <artifactId>maven-deploy-plugin</artifactId>
	          <version>2.8.2</version>
	        </plugin>
	        <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
	        <plugin>
	          <artifactId>maven-site-plugin</artifactId>
	          <version>3.7.1</version>
	        </plugin>
	        <plugin>
	          <artifactId>maven-project-info-reports-plugin</artifactId>
	          <version>3.0.0</version>
	        </plugin>
	      </plugins>
	    </pluginManagement>
	  </build>
	</project>

      

> 8 font子工程pom

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <modelVersion>4.0.0</modelVersion>
	    <groupId>pub.lgo</groupId>
	    <artifactId>tz-font</artifactId>
	    <version>0.0.1-SNAPSHOT</version>
	    <name>tz-font</name>
	    <description>Demo project for Spring Boot</description>
	    <properties>
	        <java.version>11</java.version>
	    </properties>
	
	    <!-- 子模块pom文件需要继承依赖于顶级项目中的聚合pom
	    因为使用idea构建的springboot项目的时候自动依赖了spring-boot-starter-parent
	    此时需要继承顶级项目的pom可以在聚合pom中使用springboot提供解决方案添加spring-boot-dependencies进行依赖
	    详见顶级项目中的pom配置-->
	    <parent>
	        <groupId>pub.lgo</groupId>
	        <artifactId>TAOZUI</artifactId>
	        <version>1.0-SNAPSHOT</version>
	    </parent>
	
	    <dependencies>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-web</artifactId>
	        </dependency>
	
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-test</artifactId>
	            <scope>test</scope>
	        </dependency>
	    </dependencies>
	
	    <build>
	        <plugins>
	            <plugin>
	                <groupId>org.springframework.boot</groupId>
	                <artifactId>spring-boot-maven-plugin</artifactId>
	            </plugin>
	        </plugins>
	    </build>
	</project>

	 
> 9 login子工程pom

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <modelVersion>4.0.0</modelVersion>
	    <groupId>pub.lgo</groupId>
	    <artifactId>tz-login</artifactId>
	    <version>0.0.1-SNAPSHOT</version>
	    <name>tz-login</name>
	    <description>Demo project for Spring Boot</description>
	    <properties>
	        <java.version>11</java.version>
	    </properties>
	
	    <!-- 子模块pom文件需要继承依赖于顶级项目中的聚合pom
	      因为使用idea构建的springboot项目的时候自动依赖了spring-boot-starter-parent
	      此时需要继承顶级项目的pom可以在聚合pom中使用springboot提供解决方案添加spring-boot-dependencies进行依赖
	      详见顶级项目中的pom配置-->
	    <parent>
	        <groupId>pub.lgo</groupId>
	        <artifactId>TAOZUI</artifactId>
	        <version>1.0-SNAPSHOT</version>
	    </parent>
	
	    <dependencies>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-web</artifactId>
	        </dependency>
	
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-test</artifactId>
	            <scope>test</scope>
	        </dependency>
	    </dependencies>
	    <build>
	        <plugins>
	            <plugin>
	                <groupId>org.springframework.boot</groupId>
	                <artifactId>spring-boot-maven-plugin</artifactId>
	            </plugin>
	        </plugins>
	    </build>
	</project>





## 重述

> 1 聚合工程pom需要聚合子工程使用modules标签

![](https://i.imgur.com/buPyHny.png)

> 2 聚合工程pom需要为子工程继承项目相关依赖
> springboot文档中给出的方案使用spring-boot-dependencies解决  
> 官网: [https://docs.spring.io/spring-boot/docs/1.4.3.RELEASE/reference/htmlsingle/#using-boot-maven-without-a-parent](官网:https://docs.spring.io/spring-boot/docs/1.4.3.RELEASE/reference/htmlsingle/#using-boot-maven-without-a-parent)
  
 
![](https://i.imgur.com/FFpBuWB.png) 

> 3 子工程必须继承聚合工程 

 ![](https://i.imgur.com/KoB76bK.png)  


## 问题 

### maven命令报错   
> 原因是顶级工程打包类型,因为顶级工程只为了传递依赖和聚合子工程,项目中没有java代码,
> pom的packaging类型默认是jar类型,在此只需要将聚合工程里的packaging类型修改为pom
 
![](https://i.imgur.com/HyW9Yiw.png)

![](https://i.imgur.com/smZopwt.png)



### springboot项目启动闪退
> Process finished with exit code 0   
> 应该是忘了添加spring-boot-starter-web依赖
  
![](https://i.imgur.com/SCZaTxu.png) 


![](https://i.imgur.com/DBcPuOg.png)


