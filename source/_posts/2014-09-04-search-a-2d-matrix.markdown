---
layout: post
title: "Search a 2D Matrix"
date: 2014-09-04 10:50:42 +0800
comments: true
categories: leetcode 二分
---
>Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

>* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.  

>For example,

>Consider the following matrix:

	[
	  [1,   3,  5,  7],
	  [10, 11, 16, 20],
	  [23, 30, 34, 50]
	]
>Given target = `3`, return `true`.

<!-- more-->

[leetcode express](https://oj.leetcode.com/problems/search-a-2d-matrix/)

**方法一**  
先查找target可能在的行，再从行中找target  

```c++ 二分 时间复杂度 O(logm+logn)
class Solution {
public:
    bool searchMatrix(vector<vector<int> > &matrix, int target) {
        int row = matrix.size() - 1;
        int col = matrix[0].size() - 1;
        
        //注意low从1开始
        int low = 1, high = row;
        while(low <= high)
        {
            int mid = low + (high - low)/2;
           if (matrix[mid - 1][col] == target)
                return true;
            else if (matrix[mid -1][col] > target)
                high = mid - 1;
            else
                low = mid + 1;
        }
        row = high;
        low = 0; high = col;
        while(low <= high)
        {
            int mid = (low+high)/2;
            if(matrix[row][mid] == target)
                return true;
            else if(matrix[row][mid] > target)
                high = mid -1;
            else 
                low = mid + 1;
        }
        return false;
    }
};
```

**方法二**  

这个方法还没有第一个方法好。

```c++ 时间复杂度O(n*logm)
class Solution {
public:
    bool searchMatrix(vector<vector<int> > &matrix, int target) {
        int row = matrix.size() - 1;
        int col = matrix[0].size() - 1;
        
        for(int i = 0 ; i <= row;)
        {
            int tmp = matrix[i][col];
            if(matrix[i][col] == target)
                return true;
            if(matrix[i][col] > target)
            {
                int l = 0, r = col;
                while(l <= r)
                {
                    int mid = (l+r)/2;
                    if(matrix[i][mid] == target)
                        return true;
                    if(matrix[i][mid] > target)
                        r = mid - 1;
                    else
                        l = l + 1;
                }
                return false;
            } else
            {
                i++;
            }
        }
        
        return false;
    }
};
```
