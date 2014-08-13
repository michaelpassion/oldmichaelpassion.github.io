---
author:Michael
layout: post
title: "Remove Duplicates from Sorted List II"
date: 2014-08-13 10:40:25 +0800
comments: true
categories: leetcode 链表
---
>Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. 


>For example,

>Given 1->2->3->3->4->4->5, return 1->2->5.

>Given 1->1->1->2->3, return 2->3.
<!--more-->
[Leetcode 传送门](https://oj.leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

*解题思路*

首先为链表加了一个假的头结点dummy，dummy指向head，用pre和cur两个指针去遍历；

* 如果两个指针所指节点的值不同，就加入结果链表，并用lastValidate指针指向结果链表的末尾，方便下次插入。
* 如果相同，就向后移动cur，直到cur->val != pre->val 或者 cur为空，此时需先删除pre指针所指向的节点，再用pre指向cur；如果cur不为空，就继续遍历，如果为空就跳出循环。

最后，pre可能为空，也可能是一个原链表最后一个结点，并且这个结点有效，将pre插入结果链表。用pre指向结果链表真正的头结点，删除假的头结点dummy；

``show you my code``

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
        if(!head || !head->next) return head;
        ListNode *dummy =new ListNode(head->val);
        dummy->next = NULL;
        ListNode *pre = head, *cur = head->next;
        ListNode *lastValidate = dummy;
        
        while(cur)
        {
            if(pre->val == cur->val)
            {   
                while(cur && pre->val == cur->val)
                {
                    ListNode *tmp = cur;
                    cur=!(cur->next)?NULL:cur->next;
                    delete(tmp);
                }
                    delete(pre);
                    pre = cur;
                    cur = !cur?NULL:cur->next;
            }
            else
            {
                lastValidate->next = pre;
                lastValidate = pre;
                lastValidate->next = NULL;
                pre = cur;
                cur = cur->next;
            }
        }
        lastValidate->next = pre;
        pre = dummy->next;
        delete dummy;
        return pre;
    }
};
```