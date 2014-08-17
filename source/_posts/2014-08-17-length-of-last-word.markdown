---
layout: post
title: "Length of Last Word"
date: 2014-08-17 17:24:22 +0800
comments: true
categories: leetcode 模拟
---
>Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

>If the last word does not exist, return 0.

>Note: A word is defined as a character sequence consists of non-space characters only.

>For example,

>Given s = "Hello World",

>return 5. 
<!--more-->
[leetcode express](https://oj.leetcode.com/problems/length-of-last-word/)

*思路*

###method 1

从后向前遍历，用strlen函数获取 char数组长度，具体实现如下：

```c++ method 1  8 ms 
class Solution {
public:
    int lengthOfLastWord(const char *s) {
        int i = strlen(s)-1;
        int len=0;
        
        while(i >= 0 && s[i] == ' ')
            i--;
        while(i >= 0 && s[i] != ' ')
        {
            i--;
            len++;
        }
        
        return len;
    }
};
```

###method 2 

从头开始遍历

* 如果当前字符不为空len++
* 如果当前节点为空，而下一个节点不为空，将len重置为0


```c++ method 2 32ms
class Solution {
public:
    int lengthOfLastWord(const char *s) {
        int len = 0;
        while (*s) {
            if (*s++ != ' ')
                ++len;
            else if (*s && *s != ' ')
                len = 0;

        }
        return len;
    }
};
```