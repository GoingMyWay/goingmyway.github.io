---
title: LeetCode 52. N-Queens II
date: 2017-11-07 23:54:26
tags: LeetCode
categories: LeetCode
---

## Question

Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.

![](8-queens.png)

## Solution

Same as N-Queens problem, it is a classical algorithm problem but it is not easy for newbies. To tackle this problem, we can go row by row, and in each position on each row, we can check if the current position is safe to place. So the rules are

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
        return len(self.result)

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
