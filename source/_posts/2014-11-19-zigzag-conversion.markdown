---
layout: post
title: "ZigZag Conversion"
date: 2014-11-19 19:51:18 +0800
comments: true
categories: leetcode 
---
>The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

>P   A   H   N  
A P L S I I G  
Y   I   R  
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

>string convert(string text, int nRows);
`convert("PAYPALISHIRING", 3)` should return` "PAHNAPLSIIGYIR"`.   
<!--more-->
**解题思路**
找了好长时间规律，有点乱，没有分析出合适的公式，看到这个方法，很直观，很赞，用到一个`step`变量去控制向哪一个`string`添加。而且有相当好的时间复杂度。  

```
class Solution {
public:
    string convert(string s, int nRows) {
        if (nRows < 2) return s;
        const int len = s.length();
        string res[nRows];
        int step = 1, row = 0;
        for (int i =0; i< len; i++)
        {
           res[row] += s[i];
           if (row == 0)
           {
               step = 1;
               
           }else if (row == nRows-1)
               step = -1;
            row += step;
        }
        
        for(int i=1; i< nRows; i++)
            res[0]+=res[i];
        return res[0];
    }
};
```