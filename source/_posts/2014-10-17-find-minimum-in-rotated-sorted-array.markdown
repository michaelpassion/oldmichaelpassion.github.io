---
layout: post
title: "Find Minimum in Rotated Sorted Array"
date: 2014-10-17 21:54:04 +0800
comments: true
categories: leetcode
---
>Suppose a sorted array is rotated at some pivot unknown to you beforehand.

>(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

>Find the minimum element.

>You may assume no duplicate exists in the array.   
<!--more-->

leetcode 出新题了，看起来是个水题，一时技痒就写了（不害臊，打脸）(￣ε(#￣)☆╰╮(￣▽￣///)    

**思路**  
因为是旋转的有序数组，所以可以看成是两个分别有序的递增数组，又前一个数组中的值肯定大于后一个数组中的值，所以只需遍历前面数组，找到比指向后一个数组最后一个数字小的第一个数字就是整个旋转有序数组的最小值。  
*特殊情况* ：如果原数组并没有旋转，那么`num[0] < num[n-1]`, 直接返回`num[0]`

```c++
class Solution {
public:
    int findMin(vector<int> &num) {
        if (num.size() <= 1) return num[0];
        
        int l = 0, r = num.size()-1;
        while(l < r)
        {
            if (num[l] > num[r])
                l++;
            else
                return num[l];
        }
        return num[l];
    }
};
```
