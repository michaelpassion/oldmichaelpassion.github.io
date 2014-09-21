---
layout: post
title: "Palindrome Linklist"
date: 2014-09-20 10:30:59 +0800
comments: true
categories:[cracking the coding interview], [LinkList],[链表]
---
>2.7 Implement a function to check if a linked list is a palindrome.
<!--more-->
###解法一  翻转链表得到新链表，再比较两个链表  
翻转链表的方法: 1）头插法  2）遍历加直接修改指针指向  3）递归  
```c++ 遍历加直接修改指针指向
	ListNode8 ReverList（ListNode *pHead）
	{
		ListNode *pNode = pHead; //当前结点
		ListNode *pPrev = NULL;  //当前结点的前一个结点
		while(pNode != NULL)
		{
			ListNode *pNext = pNode->next;
			PNode->next = pPrev;
			
			pPrev = pNode;
			pNode  = pNext;
		}
		return pPrev;
	}
```   
比较两个链表时，只需比较一半的元素即可，那么就要知道链表中间结点，可以通过快慢指针遍历一次得到中间结点，或者在比较的同时遍历。
```c++ 比较到中间元素
	bool isPalindrome(ListNode *aHead. ListNode *bHead)
	{
		ListNode *fast = aHead;
		
		ListNode *pa = aHead;
		ListNode *pb = bhead;		
		
		while(fast->next != NULL &&fast! = NULL)
		{
			if(*pa != *pb) return false;
			pa = pa->next;
			pb = pb->next;
		}
		return true;
	}
```
###解法二 利用栈来逆置前半个链表 
```c++
bool isPlindrome(ListNode *head)
{
	ListNode *fast = head;
	ListNode *slow = head;
	
	stack<int> a;
	//push elements from first half of linked lsit onto stack. When
	//fast runner reaches the end of the linked list, then we know we're 
	//at the middle
	
	while(fast != NULL && fast->next != NULL)
	{
		a.push(slow->val);
		slow = slow->next;
		fast = fast->next->next;
	}
	
	//the number of node is odd, skip the middle element
	if(fast != NULL)
		slow = slow->next;
	while(slow != NULL)
	{
		if(slow->val != a.top())
			return false;
		a.pop();
		slow = slow->next;
	}
	return true;
}
```
###算法三 回溯法
