---
layout: post
title: "Linked List Cycle II"
date: 2014-08-10 16:52:54 +0800
comments: true
categories: leetcode Linklist
---
>Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

>Follow up:
Can you solve it without using extra space?
<!--more-->

寻找环的过程参考 这一篇 [Linked List Cycle](https://zybuluo.com/michaelpassion/note/24977)

借用一张图，其中Y点为环的入口，由上篇可知，通过快慢指针可以发现环，假设快慢指针相交于Z点，则fast指针走过的路程为 `a+n(b+c)+b`， slow指针走过的路程为` a+b`。又 fast走过的路程为 slow 的2倍，所以 `a+n(b+c)+b = 2(a+b)` 则`a=n(b+c)-b`。 将slow指针指向head，然后slow，fast指针都以1的速度移动，slow由X点走向Y点路程为`a`, fast 路程也为`n(b+c)-b`在Y点（如果没有-b，fast指针绕了n圈又回到Z点）
![](http://images.cnitblog.com/blog/354747/201311/05171805-64db9f059a1641e7afaf3dd8223c4fe7.jpg)
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
    ListNode *detectCycle(ListNode *head) {
        if(head == NULL) return NULL;
        
        ListNode *slow = head->next;
        if (slow == NULL) return NULL;
        ListNode *fast = head->next->next;
        
        while(fast != NULL && slow != fast)
        {
            slow = slow->next;
            fast = fast->next ? fast->next->next :fast->next;
        }
        
        if(!fast) return NULL;
        slow = head;
        while(slow != fast)
        {
            slow=slow->next;
            fast=fast->next;
        }
        return slow;
    }
};
```