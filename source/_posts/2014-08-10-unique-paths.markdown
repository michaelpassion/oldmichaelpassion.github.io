---
layout: post
title: "Unique paths"
date: 2014-08-10 16:56:05 +0800
comments: true
categories:  leetcode 动态规划
---
>A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

>The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

>How many possible unique paths are there?


>Above is a 3 x 7 grid. How many possible unique paths are there?

>Note: m and n will be at most 100.
<!--more-->

*Method 1*
利用分治思想，假设矩阵A[m][n],要求A[m][n]共有多少 unique paths,可以求  
A[m][n] = A[m][n-1]+ A[m-1][n] （因为只能朝下方和右方走）
还可以用一维数组直接简化二维数组
```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        if (m > n)
        swap(m,n);
        int map[n] = {1};
        for(int i=1; i<m;++i)
        {
            for(int j=1; j<m; ++j)
                map[j]+=map[j-1];
        }
    }
}
```
*Method 2*
DP
```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
       if(m < n)
            swap(m,n);
        int a[101][101]={0};
        for(int i=0; i<m; i++)
            a[i][0] = 1;
        for(int i=1; i<n; i++)
            a[0][i] = 1;
        for(int i = 1; i<=m; i++)
            for(int j=1; j<=n;++j)
                a[i][j]= a[i-1][j] + a[i][j-1];
        return a[m-1][n-1];
    }
};
```
