---
layout:     post
title:      IDEA配置SVN
subtitle:   IDEA配置SVN
date:       2018-12-05
author:     SweetHomicide
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - IDEA
    - SVN
  
---

 
# IDEA配置SVN

## 1.安装Svn客户端
> 官网地址： https://tortoisesvn.net/downloads.html 
   下载安装64位（根据个人系统）

   ![](https://i.imgur.com/eA0ytee.png)

  
> 下一步    
  
   ![](https://i.imgur.com/Fwvrje1.png)  

> 下一步  
   
   ![](https://i.imgur.com/YIbPknb.png)

> 点击有叉的向下选择按钮
   
   ![](https://i.imgur.com/DjhOZeN.png)

> 选择第一项 will be installed on local hard drive 选项
   
   ![](https://i.imgur.com/7jaVs0I.png)

> 客户端默认安装目录是 C:\Program Files\TortoiseSVN\ 点击Next按钮下一步
   
  ![](https://i.imgur.com/O5U1I4p.png)

> 开始安装 点击install按钮进行安装
   
  ![](https://i.imgur.com/wyACdtD.png)

   ![](https://i.imgur.com/c4pvsRC.png)

> 点击finish按钮 安装完成

   ![](https://i.imgur.com/7RBARku.png)
> 此时当再次右击桌面则会看到Svn图标
   
  ![](https://i.imgur.com/poctLmQ.png)

## 2.IDEA配置SVN

>  在idea中打开设置(Ctrl+Alt+s)
    
   ![](https://i.imgur.com/VqDxeN0.png)

>  点击Version Control 选择 Subversion选项进行配置

   ![](https://i.imgur.com/WQHYhXm.png)

>  配置Use command line client为刚刚安装的SVN路径；
   
   ![](https://i.imgur.com/EccABNn.png)

>  配置完成后重新启动IDEA，从SVN库中拉去项目 (点击VCS - checkout from version control - Subversion)
   
   ![](https://i.imgur.com/OqzW8Ch.png)

   ![](https://i.imgur.com/b1C42lH.png)
   
