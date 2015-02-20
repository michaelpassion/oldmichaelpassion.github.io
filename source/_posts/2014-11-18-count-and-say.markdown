---
layout: post
title: "Count and Say"
date: 2014-11-18 22:54:58 +0800
comments: true
categories: leetcode 
---
>The count-and-say sequence is the sequence of integers beginning as follows:
`1, 11, 21, 1211, 111221, ...`

>`1` is read off as `"one 1"` or `11`.  
`11` is read off as `"two 1s"` or` 21`.  
`21` is read off as `"one 2, then one 1"` or `1211`.  
Given an integer `n`, generate the `nth` sequence.

>Note: The sequence of integers will be represented as a string.

<!--more-->


[leetcode express](https://oj.leetcode.com/problems/count-and-say/)   

**解题思路**
最开始想到递归，因为后一个字符串是通过前一个字符串确定的，但是转念一想只需要一个字符串来保存状态即可，以下解法公参考：  



```
class Solution {
public:
    string countAndSay(int n) {
        if (n == 1)  return "1";
        string a = "1";
        string tmp = "";
        for (int i=0; i< n-1; i++) {
            int count = 1;
            
            for (int j=0; j<a.length(); j++) {
                if(a[j] == a[j+1])
                    count++;
                else
                {
                    tmp += to_string(count) + a[j];
                    count=1;
    
                }
            }
            a = tmp;
            tmp = "";
        }
        
        return a;
    }
};
```