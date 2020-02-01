---
title: LeetCode 46. Permutations
date: 2017-11-08 14:28:00
tags: LeetCode
categories: LeetCode
---

## Question

Given a collection of distinct numbers, return all possible permutations.

For example,

>[1,2,3] have the following permutations:
>[
>  [1,2,3],
>  [1,3,2],
>  [2,1,3],
>  [2,3,1],
>  [3,1,2],
>  [3,2,1]
>]


## Solution

Interestingly, this problem is somewhat an easy problem, let me tell you why. For back tracking problems,
one must figure out two important point:

1. How to move forward to next state?
2. When there is no next state available for the program to move to, how to return back to the previous state?


This is part is the detailed solution to this problem, for example [1, 2, 3, 4], to get its permutations,
we can loop the list and get the current item and append it to the result list, and them loop the sub-list without the item appended before. For how to return back to the previous state, when the length of the list is zero, return. Note that, we must remove the item from the result list when all the possibile sub-permutations of the sub-list have been visited.


## Accepted Code

```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        self.results = []
        result = []
        for index, value in enumerate(nums):
            result.append(value)
            self.back_tracking(result, nums[:index]+nums[index+1:])
            result.remove(value)
        return self.results


    def back_tracking(self, result, nums):
        if len(nums) == 0:
            self.results.append(result[:])
            return


        for index, value in enumerate(nums):
            result.append(value)
            self.back_tracking(result, nums[:index]+nums[index+1:])
            result.remove(value)
```

In the code `self.back_tracking(result, nums[:index]+nums[index+1:])`, the function is to move forward to its sub-list. And `result.remove(value)` is to remove the item since all the sub-permutations of its sub-list have been visited.

