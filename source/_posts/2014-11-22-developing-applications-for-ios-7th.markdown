---
layout: post
title: "Developing Applications for iOS 7th"
date: 2014-11-22 21:37:53 +0800
comments: true
categories: Stanford_CS193p 笔记
---


###  怎么实现 `drawRect:`  
* 使用 Core Graphics  
	get a context to draw into  
	greate paths
	set colors  
	stroke or fill above create path
	
* UIBezierPath  
	* begin the path  `UIBezierPath *path = [UIbezierPath alloc] init];`
	* move around ,add lines or arcs to the path   
		```  
		path moveToPoint:CGPointMake(75, 10)];		[path addLineToPoint:CGPointMake(160, 150)];		[path addLineToPoint:CGPointMake(10, 150]);
		```
	* close the path `[path closePath]` 
	* now that the ath has been created, we can stroke/fill it  
		```
		[[UIColor greenColor] setFill];
		[[UIColor redColor] setStroke];
		[path fill];
		[path stroke];		```
		
### UIGestureRecognizer  
* This class is "abstract", we only use "concrete subclasses" of it.  
* There are two sides to using a gesture recognizer 	1. Adding a gesture recognizer to a UIView to ask it to recognize that gesture.  	2. Provinding the implementation of a method to "handle" that gesture when it happens;    
	* 通常 第一步由 controller 完成， 但是视图可以给自己添加手势  
* 第二部通常由 UIView 完成，但是 controller 可以决定以不同的方式处理一个gesture