---
title: LeetCode 51. N-Queens
date: 2017-11-07 11:18:50
tags: LeetCode
categories: LeetCode
---

## Question

The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

![](8-queens.png)

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

For example,
There exist two distinct solutions to the 4-queens puzzle:

[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]

## Solution

It is a classical algorithm problem but it is not easy for newbies. To tackle this problem, we can go row by row, and in each position on each row, we can check if the current position is safe to place. So the rules are

* if there are no Queens in vertical and horizontal direction, it is safe
* if there are no Queens in 45 diagonal direction, it is safe
* if there are no Queens in 135 diagonal direction, it is safe

And if there are no positions safe to place a Queen, return to the previous row and move onward to choose a new position in that row.


And you can watch [this video-N Queen Problem Using Backtracking Algorithm
](https://www.youtube.com/watch?v=xouin83ebxE&t=459s) on YouTube to know more about N-Queen problems.

## Accepted Code


```python
class Solution(object):
    def solveNQueens(self, n):
        """
        :type n: int
        :rtype: List[List[str]]
        """
        self.result = []
        positions = ['.'*n]*n
        self.back_tracking(n, 0, positions)
        return self.result

    def back_tracking(self, n, row, positions):
        if n == row:
            self.result.append(positions[:])
            return

        for col in range(n):
            if self.is_valid(row, col, positions):
                positions[row] = positions[row][:col] + 'Q' + positions[row][col+1:]
                self.back_tracking(n, row+1, positions)
                positions[row] = positions[row][:col] + '.' + positions[row][col+1:]

    def is_valid(self, row, col, positions):
        queen = 0
        is_safe = True
        while queen < row:
            if positions[queen].index('Q') == col or queen == row or \
                            (queen - positions[queen].index('Q')) == (row - col) or \
                            (queen + positions[queen].index('Q')) == (row + col):
                is_safe = False
                break
            queen += 1
        return is_safe
```

Note that in Python, if you want to deep copy a list, try `my_list[:]` by slicing it.

