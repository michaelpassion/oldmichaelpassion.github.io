---
layout: post
title: "Binary Tree Zigzag Level Order Traversal"
date: 2014-08-14 11:38:34 +0800
comments: true
categories: leetcode LevelTranverse 层序遍历
---

>Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

>For example:
>Given binary tree {3,9,20,#,#,15,7},
```
  	3
   / \
  9  20
    /  \
   15   7
 ```
 
>return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
```
<!--more-->
[leetcode 传送门](https://oj.leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

*思路*

层序遍历，奇数层将遍历本层结点得到的vector逆置以下再加入结果vector中。

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
    vector<vector<int> > zigzagLevelOrder(TreeNode *root) {
        vector<vector<int> > ret;
        if(!root) return ret;
        vector<TreeNode *> nodes;
        vector<int> nums;
        nodes.push_back(root);
        int cur = 0;
        int last = 1;
        bool oddlevel = true;
        while(cur < nodes.size())
        {
            last = nodes.size();
            while(cur < last)
            {
                nums.push_back(nodes[cur]->val);
                 if(nodes[cur]->right)
                    nodes.push_back(nodes[cur]->right);
                     if(nodes[cur]->left)
                    nodes.push_back(nodes[cur]->left);
                cur++;
            }
            if(oddlevel)
                reverse(nums.begin(),nums.end());
            oddlevel = !oddlevel;
            ret.push_back(nums);
            nums.clear();
                
        }
        return ret;
    }
};
```