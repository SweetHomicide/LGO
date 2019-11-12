---
layout:     post
title:      使用spring-cloud-feign客户端调用服务提供者不进行负载均衡
subtitle:   使用spring-cloud-feign客户端调用服务提供者不进行负载均衡
date:       2018-12-05
author:     SweetHomicide
header-img: img/homicide/home-bg.jpg
catalog: true
tags:
    - spring-cloud-feign
    - 微服务
    - 不进行负载均衡 
---


# 使用spring-cloud-feign客户端调用服务提供者不进行负载均衡

	说明: 
		1.启用两个服务提供者server-1 、 server-2
		2.消费端 client-1 进行feign配置,调用服务提供者的API 【去注册中心eureka中发现集群服务提供者server-1 、 server-2】
		
	问题：
		发现client-1的请求不进行负载均衡功能,每次请求client-1的消费接口都会导流到一台服务提供者上面;
	
	解决:
		@EnableEurekaClient        不会进行负载均衡功能
		@EnableDiscoveryClient       会进行负载均衡功能


	具体原因待有时间查找。
 
 

 
