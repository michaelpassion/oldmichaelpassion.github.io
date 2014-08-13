---
layout: post
title: "Spiral Matrix II"
date: 2014-08-10 22:15:15 +0800
comments: true
categories: leetcode 矩阵 Matrix
---
>Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

>For example,
Given n = 3,

>You should return the following matrix:

	[
 	 [ 1, 2, 3 ],
	 [ 8, 9, 4 ],
	 [ 7, 6, 5 ]
	]

<!--more-->
	
[leetcode 传送](https://oj.leetcode.com/problems/spiral-matrix-ii/)

---
*思路*
主要是坐标的计算，在矩阵上比划下，就很清晰了，没有什么算法思想

```c++
class Solution {
public:
    vector<vector<int> > generateMatrix(int n) {
        int level = 0;
        vector<vector<int> >matrix(n,vector<int>(n,0));
        
        int num = 1;
        while(num <= n*n)
        {
            for(int i = level; i< n-level; ++i)
                matrix[level][i] = num++;
            for(int i = level+1; i<n-level;++i)
                matrix[i][n-level-1] = num++;
            for(int i = n-2-level; i>=level;--i)
                matrix[n-1-level][i] = num++;
            for(int i = n-2-level; i>level; --i)
                matrix[i][level] = num++;
            level++;
        }
            return matrix;

    }
    
};
```
