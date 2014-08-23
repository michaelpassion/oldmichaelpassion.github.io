---
layout: post
title: "Longest Common Prefix"
date: 2014-08-22 20:26:21 +0800
comments: true
categories: leetcode Prefix
---
>Write a function to find the longest common prefix string amongst an array of strings. 
<!--more-->
[leetcode express](https://oj.leetcode.com/problems/longest-common-prefix/)

*思路*

* 从vector中找到长度最短的string，作为prefix
* 依次比较每个字串，如果前缀不同，则将prefix的最后一个字符删去，继续比较

```c++ 时间复杂度 O(mn),空间复杂度O(1)

class Solution {
public:
    string longestCommonPrefix(vector<string> &strs) {
        if (strs.size() == 0)
            return "";

        //find the shortest string's index
        //to prevent performance degradation
        int _min_len_ = strs[0].size();
        int _min_len_index_ = 0;        
        for (int i = 0; i < strs.size(); ++i)
        {
            if (strs[i].size() < _min_len_)
            {
                _min_len_ = strs[i].size();
                _min_len_index_ = i;
            }
        }


        string prefix = strs[_min_len_index_];
        for (int i = 0; i < strs.size(); ++i)
        {
            if (strs[i].find(prefix) != 0)
            {
                prefix = prefix.substr(0, prefix.size() - 1);
                --i;
            }
        }
        return prefix;
        
    }
};
```