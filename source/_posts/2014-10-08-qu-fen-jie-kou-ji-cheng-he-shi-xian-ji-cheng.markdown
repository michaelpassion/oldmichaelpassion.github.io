---
layout: post
title: "区分接口继承和实现继承"
date: 2014-10-08 10:20:06 +0800
comments: true
categories: effectvie c++ 继承 
---
<!--more-->
**成员函数的结构总是会被继承**  
public继承意味**is-a**,所以对base class为真的任何事情一定也对其derived classes为真。  
**声明一个pure virtual函数的目的是为了让 derived classes 只继承函数的接口**  
**声明impure virtual函数是为了让 derived classes 继承该函数的接口和缺省实现**  
** 声明non-virtual函数的目的是为了令 derived classes 继承函数的接口及一份强制性实现 **  

## 为多态基类声明 virtual 析构函数
***  
c++明确指出： 当derived class 对象经由一个 base class 指针删除， 而该 base class 带着一个 non-virtual 析构函数，其结果未有定义 -- 实际执行时通常发生的是对象的 derived 成分没有被销毁，然而base class 成分会被销毁，造成一个诡异的“局部销毁”的对象。  
	消除这个问题的做法是：给 base class 一个virtual 析构函数。此后删除 derived classes 对象就会调用 derived classes的析构函数

##绝对不重新定义继承而来的缺省参数值  
***  
