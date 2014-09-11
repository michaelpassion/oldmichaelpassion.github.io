---
layout: post
title: "Permutation Sequence"
date: 2014-09-11 23:48:20 +0800
comments: true
categories: leetcode permutation
---
>The set [1,2,3,…,n] contains a total of n! unique permutations.

>By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

>1. "123"  
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"  

>Given n and k, return the k-th permutation sequence.

>Note: Given n will be between 1 and 9 inclusive.  

```c++ 时间复杂度O(n),空间复杂度O(1)
class Solution {
public:
    int factorial(int n)
    {
        int res = 1;
        for(int i=2 ;i<=n; i++)
            res *= i;
        return res;
    }
    string getPermutation(int n, int k) {
        int total = factorial(n);
          string candidate = string("123456789").substr(0, n);
          string res(n,' ');
          for(int i = 0; i < n; i++)//依次计算排列的每个位
          {
              total /= (n-i);
             int index = (k-1) / total;
             res[i] = candidate[index];
             candidate.erase(index, 1);
             k -= index*total;
         }
         return res;
    }
};
```