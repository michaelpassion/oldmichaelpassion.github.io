---
layout: post
title: "Search Insert Position"
date: 2014-09-11 11:51:00 +0800
comments: true
categories: 
---
>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

>You may assume no duplicates in the array.

>Here are few examples.  
	[1,3,5,6], 5 → 2  
	[1,3,5,6], 2 → 1  
	[1,3,5,6], 7 → 4  
	[1,3,5,6], 0 → 0  
<!--more-->
[leetcode express](https://oj.leetcode.com/problems/search-insert-position/)

**思路**  
首先这题肯定用二分查找，因为给定数组是有序的，与二分不同的是如果数组中没有target要返回target应该插入的位置。在二分查找中如果没有找到target则返回-1，此时，l>r（l,r分别为标记查找范围的左指针和右指针）,而此时l = r+1, 由题目给出几组数据可知，此时l的位置就是target要应该插入的位置。

```c++ 时间复杂度O(logn),空间复杂度O(1)
class Solution {
public:
    int searchInsert(int A[], int n, int target) {
        if(n < 1) return 0;
        int l = 0, r = n - 1;
        int mid;
        
        while(l <= r)
        {
            mid = l + ((r-l)>>1);
            if(A[mid] == target) return mid;
            if(A[mid] > target)
                r = mid - 1;
            else if (A[mid] < target)
                l = mid + 1;
        }
        
        return l;
    }
};
```

**扩展**  
如果数组中有重复数字，且要求将target插入到数组中，并要在相同数字第一个位置之前，怎么设计算法？   
to be continued...