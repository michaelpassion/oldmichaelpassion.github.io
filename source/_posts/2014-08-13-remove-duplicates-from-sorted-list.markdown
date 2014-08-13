---
layout: post
title: "Remove Duplicates from Sorted List"
date: 2014-08-13 10:55:33 +0800
comments: true
categories: leetcode 链表
---
>Given a sorted linked list, delete all duplicates such that each element appear only once.

>For example,

>Given 1->1->2, return 1->2.

>Given 1->1->2->3->3, return 1->2->3.

<!--more-->

[leetcode 传送门](https://oj.leetcode.com/problems/remove-duplicates-from-sorted-list/)

这题比较简单，直接上代码


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
    ListNode *deleteDuplicates(ListNode *head) {
        if(head==NULL || head->next == NULL ) return head;
        ListNode *p = head;
        ListNode *q =p->next;
        
        while(q)
        {
            if(p->val == q->val)
            {
                ListNode *tmp = q;
                q=q->next;
                delete(tmp);
                p->next = q;
            }
            else
            {
                p = q;
                q= q->next;
            }
        }
        return head;
    }
};
```