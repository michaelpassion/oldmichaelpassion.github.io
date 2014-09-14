---
layout: post
title: "Rotate List"
date: 2014-09-14 16:08:37 +0800
comments: true
categories: leetcode 链表
---
>Given a list, rotate the list to the right by k places, where k is non-negative.  
>For example:
>Given `1->2->3->4->5->NULL` and `k = 2`,  
>return `4->5->1->2->3->NULL`.

<!--more-->
**思路**  
有点感冒，头晕晕乎乎的，还出冷汗，一开始脑子不够用，竟然套用翻转string的那个算法，还reverse三次，弱爆了。其次就是`k`的值可能大于链表长度，我没有去算链表长度，直接用快慢指针做的，这样对于特殊输入运行效率可能极其低下，回头修改，写完这点，回宿舍休息会去。

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
    ListNode *rotateRight(ListNode *head, int k) {
        if(!head || !head->next || k < 1) return head;
        ListNode *p = head;
        for (int i=0; i<k; i++) 
        {
            if (p->next == NULL) 
            {
                p = head;
            }
            else 
            {
                p = p->next;
            }
        }
        
        ListNode *q = head;
        while (p->next)
        {
            p = p->next;
            q = q->next;
        }
        p->next = head;
        
        ListNode *newHead = q->next;
        q->next = NULL;
        
        return newHead;
        }
};
```