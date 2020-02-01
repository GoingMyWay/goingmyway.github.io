---
title: LeetCode 830. Positions of Large Group
date: 2018-07-10 11:14:47
tags: LeetCode
categories: LeetCode
---

## Question

In a string `S` of lowercase letters, these letters form consecutive groups of the same character.
For example, a string like `S = "abbxxxxzyy"` has the groups `"a"`, `"bb"`, `"xxxx"`, `"z"` and `"yy"`.
Call a group large if it has 3 or more characters.  We would like the starting and ending positions of every large group.
The final answer should be in lexicographic order.

**Example 1**

```shell
Input: "abbxxxxzzy"
Output: [[3,6]]
Explanation: "xxxx" is the single large group with starting  3 and ending positions 6.
```

**Example 2**
```shell
Input: "abc"
Output: []
Explanation: We have "a","b" and "c" but no large group.
```

**Example 3**
```shell
Input: "abcdddeeeeaabbbcd"
Output: [[3,5],[6,9],[12,14]]
```

**Note:** `1 <= S.length <= 1000`


## Solution

Using two pointers, `l` and `r`, if current `nums[l]==nums[r]`, increase `r` and check if `r` reach the end.

## Code

Python code

```python
class Solution(object):
    def largeGroupPositions(self, S):
        """
        :type S: str
        :rtype: List[List[int]]
        """
        l, r = 0, 0
        result = []
        while True:
            if S[l] == S[r]:
                r += 1
                if r == len(S) and r - l >= 3:
                    result.append([l, r-1])
                    break
            else:
                if r - l >= 3:
                    result.append([l, r-1])  
                l, r = r, r
            if r == len(S):
                break
        return result
```

C++ code

```cpp
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string S) {
        vector<vector<int>> result;
        int l = 0, r = 0;
        while (1) {
            if (S[l] == S[r]) {
                r ++;
                if (r == S.size() && r - l >= 3) {
                    vector<int> _res; 
                    _res.push_back(l);
                    _res.push_back(r-1);
                    result.push_back(_res);
                    break;
                }
            } else {
                if (r - l >= 3) {
                    vector<int> _res; 
                    _res.push_back(l);
                    _res.push_back(r-1);
                    result.push_back(_res);
                }
                l = r;
            }
            if (r == S.size()) break;
        }
        return result;
    }
};
```

