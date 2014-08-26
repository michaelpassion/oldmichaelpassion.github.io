---
layout: post
title: "next_permutation"
date: 2014-08-26 13:51:45 +0800
comments: true
categories: permutation leetcode 
---
>Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.  
>If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).  
>The replacement must be in-place, do not allocate extra memory.  
>Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.  

     1,2,3 → 1,3,2 
     3,2,1 → 1,2,3 
     1,1,5 → 1,5,1
     
<!--more-->
[leetcode express](https://oj.leetcode.com/problems/next-permutation/)

*思路*  

1. 从后向前扫描 `vector<int> num`，寻找后一个数大于前一个数的位置，标记前一个数的index 为 `i`。
2. 再从后面开始扫描，寻找第一个大于下标为`num[i]`的数（必然存在，主意一定是大于没有等于符号），标记符合条件的下标为`j`,交换`num[i]` ,`num[j]`。
3. 将`index[i]`后的全部数字逆置，得到结果。


**exception**   

* 若当前数字排序已经是能表示的最大数字，所以符合条件的下一个字典序为所有排列中最小的数字


```c++
class Solution {
public:
    void nextPermutation(vector<int> &num) {
        int n = num.size();
        if(n < 2) return;
        
        for(int i = n-2, ii = n-1; i >= 0; i--, ii--)
        {
            if(num[i] < num[ii])
            {
                int j = n-1;
                while(num[j] <= num[i]) 
                    j--;
                swap(num[i],num[j]);
                reverse(num.begin()+ii,num.end());
                return;
            }
        }
        
        reverse(num.begin(), num.end());
    }
};
```