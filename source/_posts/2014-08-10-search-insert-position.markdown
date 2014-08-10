---
layout: post
title: "Search Insert Position"
date: 2014-08-10 16:51:38 +0800
comments: true
categories: leetcode 二分
---
>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

>You may assume no duplicates in the array.

>Here are few examples.

>[1,3,5,6], 5 → 2


>[1,3,5,6], 2 → 1


>[1,3,5,6], 7 → 4


>[1,3,5,6], 0 → 0
<!--more-->

代码如下，比较丑，以后更新
```c++
class Solution {
public:
    int searchInsert(int A[], int n, int target) {
        
        if(A[0] > target) return 0;
        if(A[n-1] < target) return n;
        devide(A,n,0,target);
    }
    
    int devide(int A[], int high, int low, int target)
    {
        int mid = (low + high)/2;
        
        if(A[mid] == target)
            return mid;
        else if(A[mid] > target)
        {
             devide(A,mid,0,target);
        } else if(A[mid] < target)
        {
            if(A[mid+1] > target)
                return mid+1;
            else 
                devide(A,high,mid,target);
        }
    }
};
```
