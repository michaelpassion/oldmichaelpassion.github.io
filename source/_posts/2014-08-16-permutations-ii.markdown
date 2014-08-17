---
layout: post
title: "Permutations II"
date: 2014-08-16 11:18:57 +0800
comments: true
categories: leetcode backtrack 回溯 permutation
---
 
>Given a collection of numbers that might contain duplicates, return all possible unique permutations.

>For example,

>[1,1,2] have the following unique permutations:

>[1,1,2], [1,2,1], and [2,1,1]. 
<!--more-->

[leetcode传送门](https://oj.leetcode.com/problems/permutations-ii/)

*思路*

用回溯法，求全排列的顺序同permutation

permutation

1. 首先固定首位元素，从第二位开始依次与第一位交换
2. 对去除首位的子序列，进行全排列。同样固定子序列的首位元素，从子序列的第二位起，依次与第一位交换。
3. 交换到最后一位，将此时的序列打印，递归返回。

permutation II 有重复数字，所以和相同的数字交换位置，就会得到重复的序列，通过一个无序集保存当前已经交换个位置的数，如果要交换位置的数已经在无序集中，就不交换进入下一个循环

```c++ permutation II
class Solution {
public:
    vector<vector<int> > permuteUnique(vector<int> &num) {
       vector<vector<int> > ret;
       if(num.size() < 2)
       {
           ret.push_back(num);
           return ret;
       }
       
       perm(num,ret,0);
       return ret;
    }
    
    void perm(vector<int> &num, vector<vector<int> > &ret, int t)
    {
        if(t == num.size())
        {
            ret.push_back(num);
            return;
        }
        
        unordered_set<int> used;
        for(int i=t; i< num.size(); ++i)
        {
            if(used.find(num[i]) == used.end())
            {
                swap(num[t],num[i]);
                perm(num,ret,t+1);
                swap(num[t],num[i]);
                used.insert(num[i]);
            }
        }
    }
};
```