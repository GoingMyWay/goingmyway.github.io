---
title: LeetCode 371. Sum of Two Integers
date: 2017-11-03 19:41:22
tags: LeetCode
categories: LeetCode
---

## Question

Calculate the sum of two integers a and b, but you are **not allowed** to use the operator + and -.

**Example:**
Given a = 1 and b = 2, return 3.

**Credits:**
Special thanks to @fujiaozhu for adding this problem and creating all test cases.

## Solution

Solve it in bitwise, and make sure both x and y are >= zero.

* Step 1: If you ignore the carry, say 0+0=1, 0+1=1, 1+0=1, 1+1=0, this is xor operation, ^
* Step 2: Apparently, 1+1 you will get 10, that is 10=(1&1)<<1.
* Step 3: Add the return of step 1 and step 2, and continue step 1 and step 2 until carry is 0.


## Accepted Code

```cpp
class Solution {
public:
    int getSum(int x, int y)
    {
        if ( 0 == y ) return x;
 
        int sum = x ^ y;
        int carry = (x & y) << 1;
        return getSum(sum, carry);
    }
};
```
