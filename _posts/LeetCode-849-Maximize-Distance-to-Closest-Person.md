---
title: LeetCode 849. Maximize Distance to Closest Person
date: 2018-07-10 22:59:57
tags: LeetCode
categories: LeetCode
---

## Question
In a row of `seats`, `1` represents a person sitting in that seat, and `0` represents that the seat is empty. 
There is at least one empty seat, and at least one person sitting.
Alex wants to sit in the seat such that the distance between him and the closest person to him is maximized. 
Return that maximum distance to closest person.

**Example 1:**

**Input:** [1,0,0,0,1,0,1]
**Output:** 2
**Explanation:**
If Alex sits in the second open seat (seats[2]), then the closest person has distance 2.
If Alex sits in any other open seat, the closest person has distance 1.
Thus, the maximum distance to the closest person is 2.

**Example 2:**

**Input:** [1,0,0,0]
**Output:** 3
**Explanation:**
If Alex sits in the last seat, the closest person is 3 seats away.
This is the maximum distance possible, so the answer is 3.

Note:

1. `1 <= seats.length <= 20000`
2. `seats` contains only 0s or 1s, at least one `0`, and at least one `1`.


## Solution


Using two pointers, consider three conditions

1. starting value is 0 and the ending value is 1
2. starting value is 1 and the ending value is 0
3. starting value is 1 and the ending value is 1, there is at least one 1 between them

## Code

Python

```python
class Solution(object):
    def maxDistToClosest(self, seats):
        """
        :type seats: List[int]
        :rtype: int
        """
        l, r, res, temp = 0, 0, 1, 0
        for i, v in enumerate(seats):
            if v == 0:
                r += 1
            elif v == 1:
                r = i
                if seats[l] == 0:
                    res = r - l
                else: 
                    temp = (r-l-1) / 2 if (r-l-1) % 2 == 0 else (r-l) / 2
                    
                    if temp > res:
                        res = temp
                l = i

        return res if res > r-l else r-l
```

C++ 
```cpp
class Solution {
public:
    int maxDistToClosest(vector<int>& seats) {
        int l = 0, r = 0, res = 1, dist = 0;
        for (int i = 0; i < seats.size(); i++) {
            if (0 == seats[i]) r ++;
            else {
                r = i;
                if (seats[l] == 0) res = r - l;
                else {
                    if ((r-l-1) % 2 == 0) dist = (r-l-1) / 2;
                    else dist = (r-l) / 2;
                    
                    if (dist > res) res = dist;              
                }
                l = i;
            }
        }
        return res > r-l ? res : r-l;
    }
};
```
