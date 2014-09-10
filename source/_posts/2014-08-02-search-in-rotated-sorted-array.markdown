---
layout: post
title: "Search in Rotated Sorted Array（2014-09-10 修改）"
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
**方法一**   

* 先找到两个有序子列的分界点  
* 再对两个有序子列分别使用二分查找  

``` c++ 时间复杂度O(n),空间复杂度O(1)

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
2014-09-10 修改

**方法二**   

假设数组A的左边缘为l,右边缘为r，中间元素坐标为m，分三种情况讨论  

1. 如果target == A[m], 直接返回
2. 如果A[m] < A[r]，说明后半个数组有序，分以下两种情况讨论
	* 如果target 在 A[m] 和 A[r]之间，则令 l = m + 1;
	* 否则 到数组A的前半部分查找target，令 r = m - 1;
3. 如果A[m] >= A[r], 说明数组A前半部分有序，同样分两种情况讨论
	* 如果 target 在 A[l]和 A[m]之间，则令 r = m - 1;
	* 否则，到数组A的后半部分查找target，令 l = m + 1;
	
	
```c++ 时间复杂度O(logn),空间复杂度O(1) 
class Solution {
public:
    int search(int A[], int n, int target) {
        if(n<1) return -1;
        int l = 0;
        int r = n - 1;
        while(l <= r)
        {
            int m = (l+r)/2;
            if(target == A[m]) return m;
            
            if(A[m]<A[r])
            {
                if(target > A[m] && target <= A[r])
                    l = m + 1;
                else
                    r = m - 1;
            }
            else
            {
                if(target >= A[l] && target < A[m])
                    r = m - 1;
                else
                    l = m + 1;
            }
        }
        return -1;
    }
};
```