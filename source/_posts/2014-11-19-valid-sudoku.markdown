---
layout: post
title: "Valid Sudoku"
date: 2014-11-19 17:38:58 +0800
comments: true
categories: leetcode 
---
>Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

>The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.  
![](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

>A partially filled sudoku which is valid.  
Note:A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

<!--more-->

**解题思路**  
这道题要求检查数独是否有效，既检查数独里的每一行，每一列，每一个九宫格里有没有重复数字，若有，则数独是无效的。通过一个双层循环可以实现以上三种检查，难点在检查九宫格。  
以下方法定义了三个数组，分别用来检查行，列，九宫格，相当于三个hash table。

```
class Solution {
public:
    bool isValidSudoku(vector<vector<char> > &board) {
        int checkRow[10] = {0};
        int checkCol[10] = {0};
        int checkSqu[10] = {0};
        for(int i=0; i< 9; ++i)
        {
            memset(checkRow,0,sizeof(checkRow));
            memset(checkCol,0,sizeof(checkCol));
            memset(checkSqu,0,sizeof(checkSqu));
            for(int j=0; j< 9; ++j)
            {
               if(!checkValid(checkRow,board[i][j]-'0') || 
                  !checkValid(checkCol,board[j][i]-'0') ||
                  !checkValid (checkSqu,board[3*(i/3)+j/3][3*(i%3)+j%3]-'0'))
                  return false;
                
            }
        }
        return true;
    }
    bool checkValid(int a[], int val)
    {
        if (val < 0) return true;
        if (a[val] == 1) return false;
        a[val] = 1;
        return true;
    }
};
```