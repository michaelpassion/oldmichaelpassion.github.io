---
layout: post
title: "Majority Element"
date: 2014-12-24 22:04:12 +0800
comments: true
categories: leetcode 
---
>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

>You may assume that the array is non-empty and the majority element always exist in the array.

>Credits:  
Special thanks to @ts for adding this problem and creating all test cases.
<!--more-->
[leetcode express](https://oj.leetcode.com/problems/majority-element/)  

**解题思路**     
* 本题是找数组中的 *大部分数*， 既出现次数超过数组长度 `1/2` 的数，于是：  
* 遍历整个数组，并将第一个数字记为 `check` , 后面的数字与其相同则加一， 不同则减一   
* check记录了遍历过程中，当前遍历状态下出现次数最多的数 
* 最后剩下的数字一定是出现次数超过 `1/2` 的数  



``` C++    
class Solution {
public:
    int majorityElement(vector<int> &num) {
        int check = num[0];
        int count = 1;
        for (int i = 1; i< num.size(); i++)
        {
            if (num[i] == check)
                count++;
            else {
                count--;
                if(count == 0)
                {
                    check = num[i];
                    count = 1;
                }
            }
        }
        
        return check;
    }
};
```