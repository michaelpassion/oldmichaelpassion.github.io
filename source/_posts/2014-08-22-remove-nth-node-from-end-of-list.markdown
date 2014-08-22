---
layout: post
title: "Remove Nth Node From End of List"
date: 2014-08-22 18:03:53 +0800
comments: true
categories: leetcode 链表
---
>Given a linked list, remove the nth node from the end of list and return its head.  

>For example,   

	 Given linked list: 1->2->3->4->5, and n = 2.
	 After removing the second node from the end, the linked list becomes 1->2->3->5.

>Note:

>Given n will always be valid.

>Try to do this in one pass. 
<!--more-->
[leetcode express](https://oj.leetcode.com/problems/remove-nth-node-from-end-of-list/)

*思路*

* 利用快慢指针，慢指针比快指针慢`n-1`步.
* 快指针指向最后一个结点时，慢指针指向倒数第`n+1`个结点（不能直接找倒数第n个结点，不方便删除）
* 为链表加一个多余的头结点，用来处理链表只有一个结点，并且要删除这个结点。

```c++ 时间复杂度 O(n)，空间复杂度 O(1)

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
    ListNode *removeNthFromEnd(ListNode *head, int n) {
       
        ListNode *dummy = new ListNode(-1);
        dummy->next = head;
        ListNode *slow = dummy;
        ListNode *fast = dummy;
        
        while(n > 0)
        {
            fast = fast->next;
            n--;
        }
        
        while(fast->next)
        {
            fast = fast->next;
            slow = slow->next;
        }
        
        ListNode *tmp = slow->next;
        slow->next = tmp->next;
        delete(tmp);
        tmp = dummy->next;
        delete(dummy);

        return tmp;
    }
};
```