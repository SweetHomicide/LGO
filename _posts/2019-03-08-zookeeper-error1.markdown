---
layout:     post
title:      zookpeer win10 启动闪退
subtitle:   zookpeer win10 启动闪退
date:       2018-12-05
author:     SweetHomicide
header-img: img/homicide/home-bg.jpg
catalog: true
tags:
    - zookpeer
    - win10
    - 启动闪退 
---

#zookpeer win10 启动闪退

### 版本:zookeeper-3.4.13
### 链接:http://mirror.bit.edu.cn/apache/zookeeper/zookeeper-3.4.13/
### 问题:win10 环境启动闪退

> 1.将zookeeper-3.4.13\conf下的zoo_sample.cfg 文件名重命名为 zoo.cfg

![](https://i.imgur.com/2AXQq1E.png)



> 2.打开重命名后的zoo.cfg文件 修改数据存放目录
 

![](https://i.imgur.com/ybgq5Iz.png)

> 3.去bin目录下启动 zkServer.cmd 文件

 ![](https://i.imgur.com/IEcMGTt.png)

 
