---
layout: post
title: "Reorder List"
date: 2014-08-17 16:32:11 +0800
comments: true
categories: leetcode 链表 快慢指针 翻转链表 合并链表
---
>Given a singly linked list L: ``L0→L1→…→Ln-1→Ln,``

>reorder it to: ``L0→Ln→L1→Ln-1→L2→Ln-2→…``


>You must do this in-place without altering the nodes' values.

>For example,
>Given ``{1,2,3,4}``, reorder it to ``{1,4,2,3}``. 
<!--more-->

[leetcode express](https://oj.leetcode.com/problems/reorder-list/)

*思路*

 这题的难度在于问题的规模上，需要把一个字符串划分成两个字符串（快慢指针），将第二个字符串（后半个）逆置（原地逆置，头插法），再将两个字符串合并。代码如下.
 
```c++ Reorder List

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
    ListNode* findHalfNode(ListNode *head)
    {
        ListNode *fast = head;
        ListNode *slow = head;
        
        while(fast && fast->next)
        {
            fast = fast->next->next;
            slow = slow->next;
        }
        return slow;
    }
    
    ListNode* reverseList(ListNode *head)
    {
        ListNode *dummy = new ListNode(-1);
        dummy->next = head;
        
        ListNode *cur = head->next;
        head->next = NULL;
        while(cur)
        {
            ListNode *tmp = cur;
            cur =cur->next;
            tmp->next = dummy->next;
            dummy->next = tmp;
        }
        head = dummy->next;
        delete(dummy);
        return head;
    }
    
    void mergeTwoList(ListNode *first, ListNode *second)
    {
        ListNode *pFir = first;
        ListNode *pSec = second;
        
        while(pSec)
        {
            ListNode *tmp = pSec;
            pSec = pSec->next;
            tmp->next = pFir->next;
            pFir->next = tmp;
            pFir = tmp->next;
        }
    }
    void reorderList(ListNode *head) {
        if(!head || !head->next || !head->next->next) return;
        ListNode *sec, *fir;
        
        sec = findHalfNode(head);
        fir = sec;
        sec = sec->next;
        fir->next = NULL;
        fir = head;
        sec = reverseList(sec);
        mergeTwoList(fir,sec);
        
    }
};

```