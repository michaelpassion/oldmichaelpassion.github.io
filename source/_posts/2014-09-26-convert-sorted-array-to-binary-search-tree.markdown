---
layout: post
title: "Convert Sorted Array to Binary Search Tree"
date: 2014-09-26 14:25:33 +0800
comments: true
categories: 
---


```c++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
 
 class Solution {
 public: 
 	TreeNode *array2BST(vector<int> &num, int start, int end)
 	{
 		if (start > end) return NULL;
 		
 		int mid = (start+end)/2;
 		TreeNode *root = new TreeNode(num[mid]);
 		root->left = array2BST(num,0,mid-1);
 		root->right = array2BST(num,mid+1,end);
 		
 		return root;
 	}
 	TreeNode *sortArrayToBST(vector<int> &num) {
 		return array2BST(num,0,num.size()-1);
 	}
 }
```