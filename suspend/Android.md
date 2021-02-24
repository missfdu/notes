# Android

## 预备阶段

Android应用开发特色  

1. 四大组件
   - Activity:所有应用程序的门面
   - Service:后台默默运行，即使程序退出
   - BroadcastReceiver:允许应用接收广博消息
   - ContentProvider:为应用间共享数据提供可能
2. 丰富的系统控件
3. SQLite数据库
4. 强大的多媒体

开发环境搭建

- JDK
- Android SDK
- Android Studio

## Kotlin入门

### 语言简介

2011年Jetbrains公布其第一个版本，2012年开源  
2016年Kotlin发布1.0正式版，IDEA加入对其支持  
2017年Google宣布其成为Android一级开发语言

工作原理：Kotlin代码编译成同样规格的class文件让JAVA虚拟机识别，故完全兼容JAVA

简洁高效：代码量大减，现代高级语法特性，安全性强(杜绝空指针)

### 变量和函数

声明变量：只分`val`和`var`，类型自动推导

**行尾不用加分号**

