---
layout: post
title: "Balanced Binary Tree"
date: 2014-10-07 21:54:20 +0800
comments: true
categories: 
---
>Given a binary tree, determine if it is height-balanced.

>For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.  

[leetcode express](https://oj.leetcode.com/problems/balanced-binary-tree/)

**解析**   
**算法一**   
分别去求左子树的最大深度和右子树的最大深度，若两个子树深度之差不大于1，即为平衡二叉树。  
```c++  84ms 时间复杂度o(n^2)
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
    bool isBalanced(TreeNode *root) {
        if(!root) return true;
        int left = dfs(root->left);
        int right = dfs(root->right);
        
        if(abs(left-right)>1)
            return false;
        
        return isBalanced(root->left) && isBalanced(root->right);
    }
    
    int dfs(TreeNode *root)
    {
        if(!root)
            return 0;
        return 1 + max(dfs(root->left),dfs(root->right));
    }
};
```

**算法二**   

```c++ 56 ms 时间复杂度o(n)
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

    int checkBalance(TreeNode *root) {
        if (!root) return 0;
        //check left subtree is balanced
        int leftCheck = checkBalance(root->left);
        if(leftCheck == -1)
            return -1;
        //check right subtree is balanced
        int rightCheck = checkBalance(root->right);
        if(rightCheck == -1)
            return -1;
        //check current node is balanced
        if(abs(leftCheck - rightCheck) <= 1)
            return 1 + max(leftCheck, rightCheck);
        else 
            return -1;
            
            
    }
    bool isBalanced(TreeNode *root) {
        if (checkBalance(root) == -1)
            return false;
        return true;
        
    }
    
   
};
```
