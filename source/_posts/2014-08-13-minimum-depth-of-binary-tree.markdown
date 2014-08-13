---
layout: post
title: "Minimum Depth of Binary Tree"
date: 2014-08-13 22:12:30 +0800
comments: true
categories: leetcode dfs 二叉树 递归
---
>Given a binary tree, find its minimum depth.

>The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
<!--more-->
[leetcode 传送门](https://oj.leetcode.com/problems/minimum-depth-of-binary-tree/)

*思路解析*

深度优先遍历二叉树，每遍历一层就对depth+1，如果遇到结点是叶子结点就直接返回，如果先遍历到空结点，则这个空节点这一侧不存在子树，用``INT_MAX``标记其为不可能。递归地去左右子树中找最小值。

思路比较简单，但是做了挺长时间，dfs还得加强。

``show your my code``

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
    int minDepth(TreeNode *root) {
        if(!root) return 0;
        int depth = 1;
        return dfs(root); 
    }
    
    int dfs(TreeNode *root, int depth = 1)
    {
        if(!root) return INT_MAX;
        if(!root->left && !root->right)
            return depth;
        depth++;
        return  min(dfs(root->left,depth),dfs(root->right,depth));
        
    }
};
```