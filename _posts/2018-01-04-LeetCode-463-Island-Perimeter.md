---
title: LeetCode 463. Island Perimeter
date: 2018-01-04 10:22:03
tags: LeetCode
category: LeetCode
---

## Question

You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

** Example: **

[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

Answer: 16
Explanation: The perimeter is the 16 yellow stripes in the image below:
![](island.png)

## Solution


1. Count the total number of ones
2. Count the total number of borders between ones.


## Code

```
class Solution(object):
    def islandPerimeter(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        all_count, edge_count = 0, 0
        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] == 1:
                    all_count += 1
                    if r-1 >= 0:
                        if grid[r-1][c] == 1:
                            edge_count += 1
                    
                    if r+1 <= len(grid)-1:
                        if grid[r+1][c] == 1:
                            edge_count += 1
                    
                    if c-1 >= 0:
                        if grid[r][c-1] == 1:
                            edge_count += 1
                    
                    if c+1 <= len(grid[0])-1:
                        if grid[r][c+1] == 1:
                            edge_count += 1

        return all_count*4 - edge_count
```
