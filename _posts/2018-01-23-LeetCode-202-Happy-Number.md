---
title: LeetCode 202. Happy Number
date: 2018-01-23 17:11:47
tags: LeetCode
categories: LeetCode
---

## Question

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example**: 19 is a happy number

* 1^2 + 9^2 = 82
* 8^2 + 2^2 = 68
* 6^2 + 8^2 = 100
* 1^2 + 0^2 + 0^2 = 1



## Solution

* HashTable


Since this problem is a question tagged with `HashTable`, using hash table can solve this kind of problem.

Get the sum of the squares of the input number's digits. If it equals to 1 then return `True`, no doubt it is a happy number, else store it in a hash table. If the hash table has stored it, return `False`.


* Detecting Cycled Link

Aparently, we can transfer this problem into a detecting cycled link list porblem by using a fast and a slow pointer.


## Code


* HashTable


```python
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        hash_map = {}
        while True:
            n = sum([int(v)**2 for v in str(n)])
            if n == 1:
                return True
            if n not in hash_map:
                hash_map[n] = 1
            else:
                return False
```


* Detecting Cycled LinkList

```cpp
class Solution {
public:
    bool isHappy(int n) {
        int fast = n, slow = n;
        do {
            fast = cal(cal(fast));
            slow = cal(slow);
        } while (fast != slow);
        if (1 == slow) return 1;
        else return 0;
    }
    
    int cal(int n) {
        int sum = 0;
        while (n != 0) {
            sum += (n % 10) * (n % 10);
            n /= 10;
        }
        return sum;
    }
};
```
