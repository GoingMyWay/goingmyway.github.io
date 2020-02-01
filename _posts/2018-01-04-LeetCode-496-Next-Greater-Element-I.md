---
title: LeetCode 496. Next Greater Element I
date: 2018-01-04 10:12:19
tags: LeetCode
category: LeetCode
---

## Question

You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.


The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.

** Example 1: ** 

***Input:*** nums1 = [4,1,2], nums2 = [1,3,4,2].
***Output:*** [-1,3,-1]
***Explanation:***
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.

** Example 2: **
***Input:*** nums1 = [2,4], nums2 = [1,2,3,4].
***Output:*** [3,-1]
***Explanation:***
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.

**Note:**
1. All elements in nums1 and nums2 are unique.
2. The length of both nums1 and nums2 would not exceed 1000.


## Solution

* O(n^2) version

It is simple, just loop

* O(n) version

Use stack to store the nums2, if current to be pushed value is smaller than the top value of the stack, push the value into the stack. Else pop the top value of the stack and the top value is the current value's next greater value and use hash map to store this kind of relationship.



## Code


* O(n^2) version

```python
class Solution(object):
    def nextGreaterElement(self, findNums, nums):
        """
        :type findNums: List[int]
        :type nums: List[int]
        :rtype: List[int]
        """
        outputs = []
        for v1 in findNums:
            index = nums.index(v1)
            for v2 in nums[index:]:
                if v2 > v1:
                    outputs.append(v2)
                    break
            else:
                outputs.append(-1)
        return outputs
```


* O(n) version

```python
class Solution:
    def nextGreaterElement(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        hash_map, stack = {}, []
        for v in nums2:
            if len(stack) == 0 or v <= stack[-1]:
                stack.append(v)
            else:
                while len(stack) != 0 and v > stack[-1]:
                    hash_map[stack.pop()] = v
                stack.append(v)
        return [-1 if v not in hash_map else hash_map[v] for v in nums1]
```

