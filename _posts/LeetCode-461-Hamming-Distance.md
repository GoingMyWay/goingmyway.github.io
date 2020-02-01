---
title: LeetCode 461. Hamming Distance
date: 2017-11-03 19:48:49
tags: LeetCode
categories: LeetCode
---

### Question

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

**Note:**
0 <= x, y < 2^31.

**Example:**

Input: x = 1, y = 4

Output: 2

Explanation:

```shell
1   (0 0 0 1)
4   (0 1 0 0)
       ^   ^
```
         
The above arrows point to positions where the corresponding bits are different.

### Solution


The idea is easy to understand, you should use `>>` to get the newest value, if the value is an odd number, `count += 1` , and `number = number - 1` to make it even until to `0`.

### Code

python code

```python
class Solution(object):
    def hammingDistance(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        z, count = x ^ y, 0
        
        if z == 0:
            return 0
        elif z % 2 == 0:
            return self.cal(z, count)
        else:
            count += 1
            return self.cal(z, count)
    
    def cal(self, z, count):
        while z > 0:
            z >>= 1
            if z % 2 != 0:
                count, z = count + 1, z - 1
        return count
```
