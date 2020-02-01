---
title: LeetCode 748. Largest Number At Least Twice of Others
date: 2017-12-31 12:09:24
tags: LeetCode
category: LeetCode
---

## Question

In a given integer array nums, there is always exactly one largest element.

Find whether the largest element in the array is at least twice as much as every other number in the array.

If it is, return the index of the largest element, otherwise return -1.

**Example 1:**

Input: nums = [3, 6, 1, 0]
Output: 1
Explanation: 6 is the largest integer, and for every other number in the array x,
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.

**Example 2:**

Input: nums = [1, 2, 3, 4]
Output: -1
Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.

**Note:**

1. nums will have a length in the range [1, 50].
2. Every nums[i] will be an integer in the range [0, 99].

## Solution

This question is pretty simple

1. Find the max value and its index
2. Scan through the array if `max_v < v * 2` return -1


## Code

```python
class Solution(object):
    def dominantIndex(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        max_v = max(nums)
        max_index = nums.index(max_v)

        for v in nums:
            if v != max_v and max_v < v * 2:
                return -1
        return max_index

```
