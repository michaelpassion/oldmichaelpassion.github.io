---
layout: post
title: "Linked List Cycle"
date: 2014-08-10 16:53:50 +0800
comments: true
categories: leetcode LinkList
---
>Given a linked list, determine if it has a cycle in it.

>Follow up:
Can you solve it without using extra space?
[题目地址][1]
<!--more-->
*Method 1*
快慢指针, 如果慢指针最终追上快指针，说明有环。否则，快指针先到达链表终点说明没有环。
![img][2]
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == NULL ) return false;
        ListNode *slow = head->next;
           if(slow == NULL)
            return false;
        ListNode *fast = head->next->next;
        while(fast != NULL && slow != fast)
        {
            slow =slow->next;
            fast = fast->next ? fast->next->next : fast->next;
        }
        
        if(fast != NULL)
            return true;
        else
            return false;
    }
};
```


  [1]: https://oj.leetcode.com/problems/linked-list-cycle/
  [2]: http://img.blog.csdn.net/20131105220928500?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3NfZ3VveGlhb3podQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast