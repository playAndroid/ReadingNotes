---
layout: post
title: Android studio 创建AIDL文件
date: 2016-08-14
categories: 
tags: [读书笔记]
description: Android studio 创建AIDL文件的使用
---


###Android studio 创建AIDL文件

####studio 会自动生成aidl的包并且创建一个aidl文件
![studio 会自动生成aidl的包并且创建一个aidl文件](http://img.blog.csdn.net/20160814013426608)

####接口中如果使用了其他实体类,一定要导包
![接口中如果使用了其他实体类,一定要导包](http://img.blog.csdn.net/20160814013803207)

####实体类一定要放在原包下,不要放在aidl包下,否则无法找到该类
![实体类一定要放在原包下,不要放在aidl包下,否则无法找到该类](http://img.blog.csdn.net/20160814013905428)

####点击 make project 生成相应的aidl的java文件
![点击 make project 生成相应的aidl的java文件](http://img.blog.csdn.net/20160814013532047)


####生成的aidl的java文件在此目录下
![生成的aidl的java文件在此目录下](http://img.blog.csdn.net/20160814013840801)
