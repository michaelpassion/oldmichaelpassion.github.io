---
layout: post
title: "Trapping Rain Water"
date: 2014-09-12 15:40:57 +0800
comments: true
categories: leetcode 
---
>Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

>For example,   
Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return `6`.

>![](http://www.leetcode.com/wp-content/uploads/2012/08/rainwatertrap.png)  
>The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

<!--more-->


```c++ 时间复杂度O(n), 空间复杂度O(1)
class Solution {
public:
    int trap(int A[], int n) {
        int value = 0;
        int leftMax = 0;
        int rightMax = 0;
        int l = 0, r = n-1;
        while(l <= r)
        {
            leftMax = max(leftMax, A[l]);
            rightMax = max(rightMax, A[r]);
            
            if(leftMax < rightMax)
            {
                value += leftMax - A[l];
                l++;
            }
            else
            {
                value += rightMax - A[r];
                r--;
            }
        }
        
        return value;
    }
};
```

