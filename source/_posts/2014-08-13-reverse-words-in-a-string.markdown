---
layout: post
title: "Reverse Words in a String"
date: 2014-08-13 13:09:26 +0800
comments: true
categories: leetcode reverse string 模拟
---
>Given an input string, reverse the string word by word.

>For example,

>Given s = "the sky is blue",

>return "blue is sky the".

<!--more-->
>Clarification:
What constitutes a word?
A sequence of non-space characters constitutes a word.
Could the input string contain leading or trailing spaces?
Yes. However, your reversed string should not contain leading or trailing spaces.
How about multiple spaces between two words?
Reduce them to a single space in the reversed string.

[leetcode 传送门](https://oj.leetcode.com/problems/reverse-words-in-a-string/)

*题目解析*

本来是一个不难的题目，但是做了好久，关于去除多余空格的部分想复杂了，最后参考了一名CSDN的[高手的博客](http://blog.csdn.net/kenden23/article/details/20701069)，感觉比较巧妙的地方是从后向前遍历，这样省去了不必要的操作（比如讲整个字符串逆置）。


```c++
class Solution {
public:
    
    void reverseWords(string &s) {
       string ret;
       for(int i=s.length()-1; i>=0;)
       {
           while(i>=0 && s[i] == ' ')
                --i;
            if(i < 0)
                break;
            if(!ret.empty()) ret.push_back(' ');
            string t;
            while(i>=0 && s[i] != ' ')
            {
                t+=s[i];
                --i;
            }
            reverse(t.begin(),t.end());
            ret+=t;
       }
       s = ret;
    }
};
```

剑指offer上有一题是逆置字符串单词，但是没有考虑字符串本身空格不正确的情况，假设给定的字符串是正确的英文句子（单词间有空格），书上给出的做法是先整个字符串逆置，再去从头遍历，逆置每个单词，经过两次逆置得到结果。以上方法完爆 剑指OFFER

