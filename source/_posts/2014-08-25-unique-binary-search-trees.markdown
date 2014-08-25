---
layout: post
title: "Unique Binary Search Trees"
date: 2014-08-25 20:17:26 +0800
comments: true
categories: leetcode 动态规划
---
>Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

>For example, 
>
Given n = 3, there are a total of 5 unique BST's.

<!--more-->
[leetcode express](https://oj.leetcode.com/problems/unique-binary-search-trees/)

*思路*  
二叉搜索树分为左子树，根，右子树。而每一个左子树又可继续划分为以上结构。同理右子树也可以进行同样的划分。使用一个数组来记录n个节点的二叉搜索树有多少种。后面使用时直接查询即可。

依次把每个节点作为根节点，左边节点作为左子树，右边节点作为右子树，那么总的数目等于左子树数目*右子树数目。

```c++ DP
class Solution {
public:
    int numTrees(int n) {
        int array[n+1];
        memset(array,0,sizeof(array));
        array[0] = 1;

        for(int i=1; i<=n; i++)
            for(int j=0;j<i;j++)
                array[i] += array[j]*array[i-1-j];
                
        return array[n];
    }
};
```  

实际上只需计算前半部分作为根节点的树的数目，然后乘以2（奇数节点还要加上中间节点作为根的二叉搜索树的数目）  

```c++ 只计算前半段划分
class Solution {
public:
    int numTrees(int n) {
        int array[n+1];
        memset(array,0,sizeof(array));
        array[0] = 1;

        for(int i=1; i<=n; i++)
        {
            int tmp = i>>1;
            for(int j=1;j<=tmp;j++)
            {
                array[i] += array[j-1]*array[i-j];
            }
            array[i] <<= 1;
            if(i & 0x1)
                array[i] += array[tmp] * array[tmp]; 
        }
                
        return array[n];
    }
};
```