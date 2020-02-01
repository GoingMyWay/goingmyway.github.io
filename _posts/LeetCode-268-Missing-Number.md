---
title: LeetCode 268. Missing Number
date: 2017-11-03 19:45:02
tags: LeetCode
categories: LeetCode
---

## Question

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example,
Given nums = [0, 1, 3] return 2.

**Note:**
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

**Credits:**
Special thanks to @jianchao.li.fighter for adding this problem and creating all test cases.


## Solution

Since there are `n` values taken from `0, 1, 2, ..., n` , we can use `xor` to get the missing value, for example if `n` equals 3, then the raw values are `0, 1, 2, 3`, and the `nums` for example is `0, 2, 3`. If you do `xor` operation on each item in raw values and nums one by one. 

```python
missing_value = 0^1^2^3^0^2^3   # 1
```

Since `a^0=a`, `a^a=0` and `a^b^a=a^a^b=b`.

## Accepted Code

```Python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return reduce(operator.xor, nums+range(len(nums)+1))
  ```
