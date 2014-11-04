---
layout: post
title: "近期面试题"
date: 2014-10-24 23:05:38 +0800
comments: true
categories: [面试] [objective-c][算法]
---
还是那句话最近很忙，不过这两天还好了一点了，陆陆续续的各种笔试面试参加下来，没有斩获什么offer比较失败，百度跪在了二面，面试官说我开发经验不足，这倒是真的，我的项目经历，水到不行，而且由于真实没有太多时间去搞iOS开发，所以甚至一些基础知识的东西也不是很了解。另外也许是我在写算法题的时候过于表现的太过草率了。反正就是自己不够强，多说无益，继续努力吧。
<!--more-->

UIApplication 生命周期
* * *
* `- (BOOL)application:(UIApplication *)application   willFinishLaunchingWithOptions:(NSDictionary *)launchOptions`  这个函数将会在你得App打开后主要的**storyboard**或是**nib**文件被加载后，在app状态被保存前(不甚理解)调用。当这个函数调用时，你的app处于休眠状态。   
   如果你的app是由系统出于特定原因启动的，`launchOptions`字典中的数据将指明启动的原因。出于某些原因，系统可能调用你的app的代理的附加方法。
* `- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
`  
* `- (void)applicationDidBecomeActive:(UIApplication *)application`  
* `- (void)applicationWillResignActive:(UIApplication *)application` 调用这个方法让你的app知道，它要从运行态转入不活跃。当有短信或者电话打来时或者用户退出应用应用转入后台时。处于不活跃状态的app仍然在运行指示不在向responder发送数据 
* `- (void)applicationDidEnterBackground:(UIApplication *)application`