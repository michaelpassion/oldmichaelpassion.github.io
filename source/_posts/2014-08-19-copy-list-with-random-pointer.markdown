---
layout: post
title: "Copy List with Random Pointer"
date: 2014-08-19 22:52:45 +0800
comments: true
categories: leetcode  链表
---
>A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

>Return a deep copy of the list.
<!--more-->

[参考JustDoIT的cnblog](http://www.cnblogs.com/TenosDoIt/p/3387000.html)

---

```c++ 复杂链表的复制

/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    RandomListNode *copyRandomList(RandomListNode *head) {
        if (!head) return NULL;
        
        map<RandomListNode *, RandomListNode *> oldListMap;

        RandomListNode *cur = head;
        RandomListNode *copyHead = new RandomListNode(-1);
        RandomListNode *curCopy = copyHead;
        
        
        while(cur)
        {
            oldListMap.insert(map<RandomListNode *, RandomListNode *>::value_type(cur,cur->next));
            RandomListNode *node = new RandomListNode(cur->label);
            node->random = cur;
            RandomListNode *p = cur;
            cur=cur->next;
            p->next = node;
            curCopy->next = node;
            curCopy=node;
        }
        
        curCopy = copyHead->next;
        while(curCopy)
        {
            if(curCopy->random->random)
                 curCopy->random = curCopy->random->random->next;
            else 
                curCopy->random = NULL;
            curCopy=curCopy->next;
        }
        
        cur = head;
        for(int i = 1; i<= oldListMap.size(); i++)
        {
            cur->next = oldListMap[cur];
            cur=cur->next;
        }
        return copyHead->next;
    }
};

```