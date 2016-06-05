---
layout: post
title: "iOS框架梳理"
date: 2016-06-05 10:52:16 +0800
comments: true
categories: 
---

#1.语言

##C/C++标准库相关：
\#include \<types.h>

\#include \<stddef.h>

\#include \<stdio.h>

\#include \<stdlib.h>

\#include \<string.h>


##Objective-C相关:
位于user/include/objc/目录下 

objc.h

runtime.h

objc-api.h

message.h

objc-sync.h

NSObjCRuntime.h


##Objective-C语言概念
property 

protocol

category

extension

selector


类与元类(Class & MetaClass)

内存管理(引用计数，ARC)

Key-Value编码／Key-Value观察(KVC/KVO)

Block

大中枢派发(GCD)

多线程(@synchronized)

动态绑定(Dynamic Binding)

运行时(Runtime) 


#2.CoreFoundation

##Base相关头文件:

\#include \<CoreFoundation/CFBase.h>

\#include \<CoreFoundation/CFArray.h>

\#include \<CoreFoundation/CFBag.h>

\#include \<CoreFoundation/CFBinaryHeap.h>

\#include \<CoreFoundation/CFBitVector.h>

\#include \<CoreFoundation/CFByteOrder.h>

\#include \<CoreFoundation/CFCalendar.h>

\#include \<CoreFoundation/CFCharacterSet.h>

\#include \<CoreFoundation/CFData.h>

\#include \<CoreFoundation/CFDate.h>

\#include \<CoreFoundation/CFDateFormatter.h>

\#include \<CoreFoundation/CFDictionary.h>

\#include \<CoreFoundation/CFError.h>

\#include \<CoreFoundation/CFLocale.h>

\#include \<CoreFoundation/CFNumber.h>

\#include \<CoreFoundation/CFNumberFormatter.h>

\#include \<CoreFoundation/CFPreferences.h>

\#include \<CoreFoundation/CFPropertyList.h>

\#include \<CoreFoundation/CFSet.h>

\#include \<CoreFoundation/CFString.h>

\#include \<CoreFoundation/CFStringEncodingExt.h>

\#include \<CoreFoundation/CFTimeZone.h>

\#include \<CoreFoundation/CFTree.h>

\#include \<CoreFoundation/CFURL.h>

\#include \<CoreFoundation/CFURLAccess.h>

\#include \<CoreFoundation/CFUUID.h>

\#include \<CoreFoundation/CFUtilities.h>


##MAC/iOS:

\#include \<CoreFoundation/CFBundle.h>

\#include \<CoreFoundation/CFMessagePort.h>

\#include \<CoreFoundation/CFPlugIn.h>

\#include \<CoreFoundation/CFRunLoop.h>

\#include \<CoreFoundation/CFStream.h>

\#include \<CoreFoundation/CFSocket.h>


#3.Foundation

NSRunloop

NSThread

GCD

NSOperationQueue

I/O流

文件系统

Network

CoreGraphics(CG开头)，图形图像，以CoreFoundation为基础

CoreText(CT开头)，文本渲染，以CoreGraphics，CoreFoundation为基础

CFNetwork，以CoreFoundation为基础

CoreImage，以Foundation为基础

AVFoundation，以Foundation为基础

QuartzCore(CA开头)动画，显示，UIView的后端，以Foundation为基础，继承自NSObject


#4.CocoaTouch-UIKit
贴一个UIKit类结构图：
![Alt text]({% img /images/blog/object_map.jpg %}) 

协议：

NSObject

UIStateRestoring

NSCoding

NSCopying


KVC/KVO:
(参考NSKeyValueCoding.h,NSSKeyValueObserving.h)

NSKeyValueCoding category

- (id)valueForKey:(NSString *)key;

- (void)setValue:(nullable id)value forKey:(NSString *)key;


NSSKeyValueObserving：

- (void)observeValueForKeyPath:(nullable NSString *)keyPath ofObject:(nullable id)object change:(nullable NSDictionary<NSString*, id> *)change context:(nullable void *)context;

- (void)addObserver:(NSObject *)observer forKeyPath:(NSString *)keyPath options:(NSKeyValueObservingOptions)options context:(nullable void *)context;

- (void)removeObserver:(NSObject *)observer forKeyPath:(NSString *)keyPath context:(nullable void *)context NS_AVAILABLE(10_7, 5_0);

- (void)removeObserver:(NSObject *)observer forKeyPath:(NSString *)keyPath;



#Tips
>###nil/Nil/null/NULL/NSNull的比较
>1.nil 空的NSObject实例对象 
>\#define nil __DARWIN_NULL
>\#define __DARWIN_NULL ((void *)0)  

>2.Nil 空的NSObject类对象
>define Nil __DARWIN_NULL 

>3.null/NULL
>\#define NULL ((void*)0)  指向0地址的指针

>4.NSNull 
>一个代表空值的NSObject类，常用于集合中的占位对象

>结论：
>(1)1nil=Nil=Null=NULL=(void *)0
>(2)[nil message]返回NO，无异常抛出
>(3)[NSNull message]抛出异常NSException


