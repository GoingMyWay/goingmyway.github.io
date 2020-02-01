---
title: LeetCode 665. Non-decreasing Array
date: 2017-11-03 19:19:51
tags: LeetCode
categories: LeetCode
---

## Question

Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.

We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n).

**Example 1:**

Input: [4,2,3]
Output: True
Explanation: You could modify the first 
 4
 to 
 1
 to get a non-decreasing array.

**Example 2:**

Input: [4,2,1]
Output: False
Explanation: You can not get a non-decreasing array by modify at most one element.

**Note:** The n belongs to [1, 10,000].


## Solution

For this problem, We should count how many times the items of the array have been changed. So my idea is to compare `nums[i]` with `nums[i-1]`  and if  `nums[i] < nums[i-1]` then set `nums[i-1]` with `nums[i]` . However the problem is not that easy, some conditions should take into consideration, for example

* Condition One: `nums[i] > nums[i-2]` 

```python
  i-2 i-1   i 
1   2   8   4 
```

  Here `nums[i] > nums[i-2]`, so replace `nums[i-1]` with `nums[i]`, that is `nums[i-1] = nums[i]`

* Condition Two: `nums[i] < nums[i-2]`

```python
  i-2 i-1   i 
1   3   3   2   4
```

Here `nums[i] < nums[i-2]`, so replace `nums[i]` with `nums[i-1]`, that is `nums[i] = nums[i-1]`

As you can see, the key problem is which item should be replaced `nums[i]` or `nums[i-1]` and what value should be set.


## Accepted Code


```python
class Solution(object):
    def checkPossibility(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        change_count = 0
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                if i-1 >= 1:
                    if nums[i] >= nums[i-2]:
                        nums[i-1] = nums[i]
                    else:
                        nums[i] = nums[i-1]
                    change_count += 1
                else:
                    nums[i-1] = nums[i]
                    change_count += 1
                    
                if change_count >= 2:
                    return False

        return True

```
