---
layout: post
title: "Palindrome Number"
date: 2014-08-22 18:59:43 +0800
comments: true
categories: 
---
>Determine whether an integer is a palindrome. Do this without extra space.

>Some hints:

>Could negative integers be palindromes? (ie, -1)

>If you are thinking of converting the integer to string, note the restriction of using extra space.

>You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

>There is a more generic way of solving this problem.

<!--more-->

[leetcode express](https://oj.leetcode.com/problems/palindrome-number/)

根据提示知：

* 负数肯定不是回文数字
* 如果将数字转换为字符串，则使用了额外空间，不符合题目要求
* 每次选取最高位和最低位比较，如果不同，则返回false
* 如果最高位和最低位相同，则将该数字转换为减去最高位和最低位的数字(外观上，实际需要数学操作)

``` c++ 时间复杂度 O(n), 空间复杂度 O(1)

class Solution {
public:
    bool isPalindrome(int x) {
        if(x < 0) return false;
        
        int div =1;
        while( x / div >= 10) {
            div *= 10;
        }
        
        while(x != 0)
        {
            int l = x / div;
            int r = x % 10;
            if(l != r) return false;
            x = (x % div) /10;
            div /= 100;
        }
        
        return true;
    }
};
```