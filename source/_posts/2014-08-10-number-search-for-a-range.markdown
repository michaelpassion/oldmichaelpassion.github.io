---
layout: post
title: "# Search for a Range"
date: 2014-08-10 16:48:21 +0800
comments: true
categories: leetcode 二分
---
>Given a sorted array of integers, find the starting and ending position of a given target value.

>Your algorithm's runtime complexity must be in the order of O(log n).

>If the target is not found in the array, return [-1, -1].

>For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
<!--more-->
[原题传送门](https://oj.leetcode.com/problems/search-for-a-range/)

*解析*
因为数组是有序的，所以可以使用二分去查找。其实本题是二分的变形。
```c++
class Solution {
public:
    vector<int> searchRange(int A[], int n, int target) {
        
      vector<int> ret(2,-1);
      if(n == 0 || A[0]>target || A[n-1]<target)
            return ret;
        int low=0,high=n-1;
        int mid = (low+high)/2;
        
        //第一次二分，找target
        while(low<=high)
        {
            mid = (low+high)/2;
            if(A[mid] == target)
            {
                ret[0]=mid;
                ret[1]=mid;
                break;
            }
            else if (A[mid] > target)
            {
                high = mid-1;
            }
            else 
                low = mid +1;
        }
        if(A[mid] != target)
            return ret;
        //第二次二分找target的右边界
        int newL = mid;
        int newR = n-1;
        while(newL <= newR)
        {
            int newMid = (newR+newL)/2;
            if(A[newMid] == target)
                newL = newMid+1;
            else
                newR = newMid-1;
        }
        
        ret[1] = newR;
        //第三次二分找target的左边界
        newL=0;
        newR=mid;
        while(newL<=newR)
        {
            int newMid = (newL+newR)/2;
            if(A[newMid] == target)
                newR = newMid-1;
            else
                newL = newMid+1;
        }
        
        ret[0] = newL;
        return ret;
    }
};
```


