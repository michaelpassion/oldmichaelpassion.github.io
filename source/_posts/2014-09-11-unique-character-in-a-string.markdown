---
layout: post
title: "Unique Character in a String"
date: 2014-09-11 17:34:37 +0800
comments: true
categories: [算法, Cracking the Coding Interview, 位操作]
---
>Implement an algorithm to determine if a string has all unique characters. What if you cannot use additional data structures?  
<!--more-->

```c++ 空间复杂度O(1),时间复杂度O(n)
bool isUnique(string s)
{
	int len = s.length();
	if(len > 256) return false; //以ASCII讨论，ASCII总数为256，如果字符串的长度大于256，
								 //肯定有重复字符
	bool check[256];
	memset(a,false,sizeof(a));
	for(int i=0; i<len; i++)
	{
		if(check[i])
			return false;
		check[i] = true;
	}
	return true;
}
```  
如果字符串中所有字符全是小写字母（a-z）,字符总数为26，为节省空间，还可以将字符映射到int的每一位上。  
```c++ 空间复杂度O(1),时间复杂度O(n) 位操作
bool isUnique(string s)
{
	int len = s.length();
	if(len > 26) return false;
	
	int checker = 0;
	
	for(int i=0; i<len; i++)
	{
		int val = s[i]-'a';
		if((checker & (1<<val)) > 0)
			return false;
		checker |= (1<<val);
	}
	
	return true;
}
```