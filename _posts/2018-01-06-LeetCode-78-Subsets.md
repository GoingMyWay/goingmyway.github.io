---
title: LeetCode 78. Subsets
date: 2018-01-06 12:21:09
tags: LeetCode
category: LeetCode
---


## Question

Given a set of distinct integers, nums, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]


## Solution

This problem is a backtracking problem, using depth first search can solve this problem.

## Code

DFS C++ version

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> path;
        dfs(nums, 0, path, result);
        return result;
    }
    
    void dfs(vector<int>& nums, int index, vector<int>& path, vector<vector<int>> & result) {
        result.push_back(path);
        for (int i=index; i < nums.size(); i ++) {
            path.push_back(nums[i]);
            dfs(nums, i+1, path, result);
            path.pop_back();
        }
    }
};
```

DFS Python version

```python
class Solution:
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        outputs = []
        self.dfs(sorted(nums), 0, [], outputs)
        return outputs
        
    def dfs(self, nums, index, path, outputs):
        outputs.append(path)
        for i in range(index, len(nums)):
            self.dfs(nums, i+1, path+[nums[i]], outputs)
```
