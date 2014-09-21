---
layout: post
title: "Word Search"
date: 2014-09-21 13:47:52 +0800
comments: true
categories: leetcode dfs
---
>Given a 2D board and a word, find if the word exists in the grid.

>The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

>For example,  
Given board =   
>
	[
	  ["ABCE"],
	  ["SFCS"],
	  ["ADEE"]
	]	
>word = `"ABCCED"`, -> returns `true`,  
word = `"SEE"`, -> returns `true`,  
word = `"ABCB"`, -> returns `false`.
<!--more-->
**思路**  
先在board中寻找word的首字母，找到后在该位置的相邻位置（上下左右）查看是否能生成word，如果上下左右中有位置符合条件，则继续从该位置的临近位置搜索下一个字符。主要，不能board中的字符不能重复使用，故需要将访问过的字符做标记，下面代码中设置为`‘#’`,对该位置搜索完后要恢复原来的字母。  

```c++
class Solution {
public:

    bool dfs(vector<vector<char>> &board,int row, int col, string word, int index)
    {
        if (index == word.size()-1) return true;
        char ctmp = board[row][col];
        board[row][col] = '#';
        
        //向上查询
        if (row-1>=0 && board[row-1][col] == word[index+1])
            if (dfs(board,row-1,col,word,index+1))
                return true;
         
         //向下
        if (row+1<=board.size()-1 && board[row+1][col] == word[index+1])
            if (dfs(board,row+1,col,word,index+1))
                return true;
        //向左
        if (col-1 >= 0 && board[row][col-1] == word[index+1])
             if (dfs(board,row,col-1,word,index+1))
                return true;
        向右
        if(col+1 <= board[0].size()-1 && board[row][col+1] == word[index+1])
            if (dfs(board,row,col+1,word,index+1))
                return true;
                
        //恢复原来的字母        
        board[row][col] = ctmp;
        return false;
    }
    bool exist(vector<vector<char> > &board, string word) {
        const int rows = board.size();
        const int cols = board[0].size();
        
        for (int i=0; i<rows; i++)
        {
            for (int j=0; j<cols; j++)
            {
                if (board[i][j] == word[0] && dfs(board,i,j,word,0))
                    return true;
            }
        }
        
        return false;
    }
};
```