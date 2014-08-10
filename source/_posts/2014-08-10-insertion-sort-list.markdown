---
layout: post
title: "Insertion Sort List"
date: 2014-08-10 19:35:54 +0800
comments: true
categories: leetcode  链表
---
>Sort a linked list using insertion sort.
<!--more-->
[leetcode 传送门](https://oj.leetcode.com/problems/insertion-sort-list/)

---
*思路*
过程比较清晰的链表操作题，一开始提交出现RE，看了下原来是

` while(p->next && p->next->val < cur->val)` 写成了

` while(p->next->val < cur->val && p->next)` 如果不先判断Node是否为空就去取值必然出现问题。

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
    ListNode *insertionSortList(ListNode *head) {
        
        ListNode *p = head;
        if(p == NULL || p->next == NULL) return head;
        
        ListNode *dummy = new ListNode(-1);
        dummy->next = head;
        ListNode *cur = head->next;
        head->next = NULL;
        
        while(cur)
        {
            ListNode *p = dummy;
            while(p->next && p->next->val < cur->val)
            {
                p=p->next;
            }
           
            ListNode *tmp = cur;
            cur=cur->next;
            tmp->next = p->next;
            p->next = tmp;
        }
        return dummy->next;
        
    }
};
```