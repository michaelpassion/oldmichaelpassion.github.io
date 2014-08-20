---
layout: post
title: "Longest Palindromic Substring"
date: 2014-08-20 15:21:20 +0800
comments: true
categories: leetcode 分治 
---
>Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

<!--more-->
[leetcode express](https://oj.leetcode.com/problems/longest-palindromic-substring/)

###本文参考 cnblog博主[tenos 博客](www.cnblogs.com/TenosDoIt/p/3675788.html)

*解法一*

``` c++ Longest Palindromic Substring 时间复杂度O（n^2）,空间O（n^2）

class Solution {
public:
    string longestPalindrome(string s) {
         const int len = s.size();
        if(len <= 1)return s;
        bool dp[len][len];//dp[i][j]表示s[i..j]是否是回文,如果用vector来表示这个数组会超时
        memset(dp, 0, sizeof(dp));
        int resLeft = 0, resRight = 0;
        dp[0][0] = true;
        for(int i = 1; i < len; i++)
        {
            dp[i][i] = true;
            dp[i][i-1] = true;//这个初始化容易忽略，当k=2时要用到
        }
        for(int k = 2; k <= len; k++)//枚举子串长度
            for(int i = 0; i <= len-k; i++)//枚举子串起始位置
            {
                if(s[i] == s[i+k-1] && dp[i+1][i+k-2])
                {
                    dp[i][i+k-1] = true;
                    if(resRight-resLeft+1 < k)
                    {
                        resLeft = i;
                        resRight = i+k-1;
                    }
                }
            }
        return s.substr(resLeft, resRight-resLeft+1);
    }
};
```
*解法二*

以某个元素为中心，分别计算偶数长度的回文最大长度和奇数长度的回文最大长度。时间复杂度O(n^2)，空间O（1）

``` c++ Longest Palindromic Substring 时间复杂度O(n^2)，空间O（1）
class Solution {
public:
    string longestPalindrome(string s) {
         const int len = s.size();
        if(len <= 1)return s;
        
        int start = 0, maxLen = 0;
        for(int i=1; i< len; ++i)
        {
            //寻找以i-1,i为中心的偶数长度的回文
            int low = i-1, high = i;
            while(low >=0 && high < len && s[low] == s[high])
            {
                low--;
                high++;
            }
            if(high - low - 1 > maxLen)
            {
                start = low+1;
                maxLen = high - low -1;
            }
            
            //寻找以i为中心的奇数长度的回文
            low = i-1; high = i+1;
            while(low >=0 && high < len && s[low] == s[high])
            {
                low--;
                high++;
            }
            
            if(high - low -1 > maxLen)
            {
                maxLen = high - low - 1;
                start = low + 1;
            }
        }
        return s.substr(start, maxLen);
    }
};
```
*解法3 Manacher算法*

>该算法首先对字符串进行预处理，在字符串的每个字符前后都加入一个特殊符号，比如字符串abcd处理成 #a#b#c#d# ，为了避免处理越界，在字符串首位加上两个不同的特殊字符（此类型的字符串尾部不用加，自带‘\0’），这样预处理后最终便车工$#a#b#c#d#^,经过这样处理，原来的偶数长度的回文和奇数长度的回文在处理后的字符串都是奇数长度，假设处理后的字符串为s，对于已经预处理的字符串我们用数字p[i]来记录以字符s[i]为中心的最长回文字串向右或向左扩展的长度（包括s[i]），以字符串“12212321”为例，p数组如下：

	s: $ # 1 # 2 # 2 # 1 # 2 # 3 # 2 # 1 # ^
	p:   1 2 1 2 5 2 1 4 1 2 1 6 1 2 1 2 1
	
可以看出，P[i]-1正好是原字符串中回文串的总长度, 如果p数组已知，遍历p数组找到最大的p[i]就可以求出最长回文的长度，也可以求出回文的位置 

下面给出求p[]数组的方法：

设id是当前求得的最长回文子串中心的位置，mx为当前最长回文子串的右边界（回文子串不包括该右边界），即mx = id + p[id]。记j = 2*id – i ，即 j 是 i 关于 id 的对称点。

1. 当i < mx 时，如下图。此时可以得出一个非常神奇的结论p[i] >= min(p[2*id - i], mx - i)，下面我们来解释这个结论

![](http://images.cnitblog.com/blog/517264/201404/192355300257453.png)

如何根据p[j]来求p[i]?要分两种情况：

  * 当mx-i>p[j]，这时候以s[j]为中心的回文字串包含在以s[id]为中心的回字串中，由于i和j对称，以s[i]为中心的回文字串必然包含在以s[id]为中心的回文字串中，所以p[i]至少等于p[j]，如下图：
  
  **注：这里其实p[i]一定等于p[j],后面不用再匹配了。因为如果p[i]后面还可以继续匹配，根据对称性，p[j]也可以继续扩展了**
 
 ![](http://images.cnitblog.com/blog/517264/201404/192355308851026.png)
 
 * 当i >= mx, 无法对p[i]做更多的假设，只能p[i] = 1,然后再去匹配
 
 算法复杂度分析：根据斜体字部分的注释，只有当mx-i = p[j]时 以及 i > mx时才要扩展比较，而mx也是在不断扩展的，总体而言每个元素比较次数是n的线性关系，所以时间复杂度为O(n)



```c++ Manacher算法，时间复杂度O(n), 空间复杂度O(n)
class Solution {
public:
    string longestPalindrome(string s) {
        const int len = s.size();
        if(len <= 1)return s;
        //Manncher算法 ，o（n）
        string str = preProcess(s);
        int n = str.size(), id = 0, mx = 0;
        vector<int>p(n, 0);
        for(int i = 1; i < n-1; i++)
        {
            p[i] = mx > i ? min(p[2*id-i], mx-i) : 1;
            //if(mx <= i || (mx > i && p[2*id-i] == mx - i)) //根据正文斜体部分的注释，这里可要可不要
            while(str[i+p[i]] == str[i-p[i]])p[i]++;
            if(i + p[i] > mx)
            {
                mx = i + p[i];
                id = i;
            }
        }
         
        //遍历p，寻找最大回文长度
        int maxLen = 0, index = 0;
        for(int i = 1; i < n-1; i++)
            if(p[i] > maxLen)
            {
                maxLen = p[i];
                index = i;
            }
        return s.substr((index - maxLen)/2, maxLen-1);
    }
    //预处理字符串，abc预处理后变成$#a#b#c#^
    string preProcess(const string &s)
    {
        int n = s.size();
        string res;
        res.push_back('$');//把$放到字符串头部
        res.push_back('#');//以#作为原来字符串中每个字符的间隔
        for(int i = 0; i < n; i++)
        {
            res.push_back(s[i]);
            res.push_back('#');
        }
        res.push_back('^');//以^作为字符串的结尾
        return res;
    }
};
``` 