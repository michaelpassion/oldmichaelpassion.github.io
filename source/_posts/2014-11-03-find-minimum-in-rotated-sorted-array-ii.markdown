---
layout: post
title: "Find Minimum in Rotated Sorted Array II"
date: 2014-11-03 23:22:11 +0800
comments: true
categories: 
---
>Follow up for "Find Minimum in Rotated Sorted Array":  
What if duplicates are allowed?  

>Would this affect the run-time complexity? How and why? 

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates. 
<!--more--> 

**思路**  
由于是旋转数组，可以说基本有序，可以用二分的方法去筛去最小值肯定不存在的部分。  
```c++  时间复杂度O(logn) 
class Solution {
public:
    int findMin(vector<int> &num) {
        int len = num.size();
        if (len < 2) return num[0];
        return findHelper(num,0,len-1);
        
    }
    
    int findHelper(vector<int> &num,int start, int end)
    {
        if(start < end)
        {
            int mid = start+ (end-start)/2;
            
            // 3,1,3,3 情况
            if (num[mid] == num[start] && num[mid] == num[end])
            {
                int a = findHelper(num,start,mid);
                int b = findHelper(num,mid+1,end);
                return a <= b ? a : b;
            }
            // 1,3,3
            else if (num[mid] >= num[start] && num[start] >= num[end])
                return findHelper(num,mid+1,end);
             // 
            else if (num[mid] >= num[start] && num[start] <= num[end])
                 return findHelper(num,start,mid);
            else if (num[mid] <= num[start] && num[mid]<= num[end])
                return findHelper(num,start,mid);
        } 
        return num[start];
    }
};
```

**非递归方法**  
```c++
class Solution {
public:
    int findMin(vector<int> &num) {
        if (num.size() < 2) return num[0];
        
        int l =0, r= num.size()-1, mid = l+(r-l)/2;
        while(l < r)
        {
            mid = l+(r-l)/2;
            if (num[mid] == num[l] && num[mid] == num[r])
            {
                while (l < r && num[mid] == num[l] && num[mid] == num[r] )
                {
                    l++;
                    r--;
                }
            }
            else if (num[mid] >= num[l] && num[mid] > num[r])
            {
                l = mid+1;
            }
            else if (num[mid] <= num[l] && num[mid] <= num[r])
            {
                r = mid;
            }
            else if (num[mid] >= num[l] && num[mid] <= num[r])
                r = mid - 1;
             
        }
        
        return num[l];
    }
};
```   

以上两个方法，都不是很优雅，对于特殊情况的判断是根据oj提供的错误信息，经过几次改正才得到的结果，不是很清晰，可能oj提供的case不足以证明这两个方法的正确性，若各位发现错误，或有好的建议，欢迎留言 XD 。

***Much better way***

```c++
	class Solution {
public:
    int findMin(vector<int> &num) {
        int len = num.size();
        if (len < 2) return num[0];
        int l = 0, r = len-1;
        
        while(l < r && num[l] >= num[r])
        {
            int mid = (l + r)/2;
            if (num[mid] > num[l])
                l = mid + 1;
            else if (num[mid] < num[r])
                r = mid;
            else
                l = l+1;
        }
        return num[l];
    }
};```