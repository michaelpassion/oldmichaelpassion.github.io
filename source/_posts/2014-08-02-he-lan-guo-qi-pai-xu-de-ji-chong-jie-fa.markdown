---
layout: post
title: "荷兰国旗排序的几种解法"
date: 2014-08-02 19:32:51 +0800
comments: true
categories: 
---
>Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

>Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

>Note:
You are not suppose to use the library's sort function for this problem.
<!--more-->


[leetcode Sort Colors][1]


*Method 1*
统计各颜色出现的次数，然后重新给颜色数组赋值

```c++
//时间复杂度 O(n),空间复杂度O(1)
class Sloution {
public:
    void sortColorts(int A[], int n) {
        int colors[3]={0};
        for( int i = 0; i < n; ++i)
            colors[A[i]]++;
        for(int i = 0, index =0; i < 3; ++i)
        {
            for(int j=0; j< colors[i]; ++j)
                A[index++] = i;
        }
    }
}
```
*Method 2*
利用快速排序的思想,遍历，交换元素

```c++
//时间复杂度 O(n),空间复杂度O(1)
class Solution {
public:
    void sortColors(int A[], int n) {
        int begin = 0, cur = 0, end = n-1;
        while(cur != end)
        {
            if(A[cur] == 0)
            {
                swap(A[begin],A[cur]);
                begin++;
                cur++;
            } else if(A[cur] == 1)
            {
                cur++;
            } else
            {
                swap(A[cur], A[end]);
                end--;
            }
        }
    }
};
```

*Method 3*
同样维护三个指针，指向0，1，2的三个数组的起始位置。如果下一个数字是0，向右移动1,2两个指针的位置，将0放到合适的位置。移动指针时，并没有移动整个数组，只需要3个位置需要改变。 1和2同上

```c++
//时间复杂度 O(n),空间复杂度O(1)
class Solution {
public:
    void sortColors(int A[], int n) {
        int i=-1,j=-1,k=-1;
        for(int p = 0; p < n; ++p)
        {
            if(A[p] == 0)
            {
                A[++k] = 2;
                A[++j] = 1;
                A[++i] = 0;
            }
            else if (A[p] == 1)
            {
                A[++k] = 2;
                A[++j] = 1;
            }
            else if (A[p] == 2)
            {
                A[++k] = 2;
            }
        }
    }
};
```

*Method 4*
两个指针，和快排的解法一样

```c++
//时间复杂度O(n)，空间复杂度O(1)
class Solution {
public:
    void sortColors(int A[], int n) {
        int red = 0, blue = n-1;
        for （int i = 0; i < n; ++i)
        {
            if(A[i] == 0)
                swap(A[i++], A[red++]);
            else if (A[i] == 2)
            {
                swap(A[i++],A[blue--]);
            }
            else
            {
                i++;
            }
        }
    }
};
```
  [1]: https://oj.leetcode.com/problems/sort-colors/