---
layout: post
title: "Add Binary"
date: 2014-11-19 13:11:32 +0800
comments: true
categories: leetcode Bit Manipulation 
---
>
Given two binary strings, return their sum (also a binary string).

>For example,  
a = `"11" `  
b = `"1" `  
Return `"100"`.

<!--more-->
[leetcode express](https://oj.leetcode.com/problems/add-binary/)

**解题思路**
类似于多项式相加，用位运算加速计算，`carry`用来保存进位，`tmp`保存两个二进制数第`i`位的和，再和carry相加，并将结果加入`res`中，最后因为`res`是逆序的，再将`res`翻转一遍。  
```
class Solution {
public:
    string addBinary(string a, string b) {
        int result=0, carry =0;
        string res = "";
        int aLen = a.length()-1;
        int bLen = b.length()-1;
        int tmp;
        
        while(aLen >=0 && bLen >=0)
        {
            result = (a[aLen]-'0')^(b[bLen] - '0');
            tmp = (result ^ carry);
            res +=to_string(tmp);
            carry = (a[aLen--]- '0')+(b[bLen--] - '0')+carry >= 2 ? 1 : 0;
        }
        
        while (aLen>=0) {
            tmp = ((a[aLen]-'0')^carry);
            res += to_string(tmp);
            carry = (a[aLen]-'0')&carry;
            aLen--;
        }
        while (bLen>=0) {
            tmp = ((b[bLen]-'0')^carry);
            res += to_string(tmp);
            carry = (b[bLen]-'0')&carry;
            bLen--;
        }
        if (carry == 1) {
            res += to_string(carry);
        }
        
        int l =0, r= res.length()-1;
        while(l < r)
        {
            swap(res[l],res[r]);
            l++;r--;
        }
    
        return res;
    }

};
```