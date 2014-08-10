---
layout: post
title: "Search in Rotated Sorted Array.md"
date: 2014-08-02 19:16:49 +0800
comments: true
categories: leetcode 二分

---

>Suppose a sorted array is rotated at some pivot unknown to you beforehand.

>(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

>You are given a target value to search. If found in the array return its index, otherwise return -1.

>You may assume no duplicate exists in the array
<!--more-->


---
```c++
class Solution {
public:
    int search(int A[], int n, int target) {
        int p = 0;
        while(p<n-1)
        {
            if(A[p]<A[p+1])
                p++;
            else
                break;
        }
        
        
        if(p == n-1 )
        {
            int low=0;
            int high =p;
            while(low <= high)
            {
                int mid = (low + high)/2;
                if(A[mid] == target)
                    return mid;
                else if(A[mid] > target)
                    high = mid -1;
                else
                    low = mid +1;
            }
            return -1;
        }
        int low=0;
        int high =p;
        while(low <= high)
        {
            int mid = (low + high)/2;
            if(A[mid] == target)
                return mid;
            else if(A[mid] > target)
                high = mid -1;
            else
                low = mid +1;
        }
        
    
        low = p+1;
        high = n-1;
        while(low <= high)
          {
            int mid = (low + high)/2;
            if(A[mid] == target)
                return mid;
            else if(A[mid] > target)
                high = mid -1;
            else
                low = mid +1;
        }
        
        return -1;
    }
```
