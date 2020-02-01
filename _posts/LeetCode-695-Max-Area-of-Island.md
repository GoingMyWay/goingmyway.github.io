---
title: LeetCode 695. Max Area of Island
date: 2017-12-21 10:03:02
tags: LeetCode
categories: LeetCode
---

Hi, again, I was very busy these days. Today's LeetCode question is very simple-Depth-First Search. Here is the question.

## Question

Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

** Example 1: **

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.

** Example 2: **

```
[[0,0,0,0,0,0,0,0]]
```

Given the above grid, return 0.
Note: The length of each dimension in the given grid does not exceed 50.

## Solution

This is a Deepth-first Search problem, so it is simple to tackle by using recursion.


## Code

```python
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        max_area = 0
        for row in range(len(grid)):
            for col in range(len(grid[0])):
                max_area = max(self.dfs(grid, row, col, 0), max_area)
        return max_area


    def dfs(self, grid, row, col, area):
        if grid[row][col] == 0:
            return 0
        
        grid[row][col] = 0
        area += 1

        if row+1 < len(grid) and grid[row+1][col] == 1:
            area = self.dfs(grid, row+1, col, area)

        if row-1 >= 0 and grid[row-1][col] == 1:
            area = self.dfs(grid, row-1, col, area)

        if col-1 >= 0 and grid[row][col-1] == 1:
            area = self.dfs(grid, row, col-1, area)

        if col+1 < len(grid[0]) and grid[row][col+1] == 1:
            area = self.dfs(grid, row, col+1, area)

        return area

```

