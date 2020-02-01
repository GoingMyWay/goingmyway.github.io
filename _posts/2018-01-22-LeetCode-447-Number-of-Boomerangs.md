---
title: LeetCode 447. Number of Boomerangs
date: 2018-01-22 10:23:11
tags: LeetCode
categories: LeetCode
---


## Question

Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points `(i, j, k)` such that the distance between `i` and `j` equals the distance between `i` and `k` (the order of the tuple matters).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).


## Solution

At the first sight, I thought this problem is a math problem, to get all the vectors which is perpendicular to the other vector. Intuitively, it is a nice solution, however, it is very time consuming. So, here using hashMap is a better solution because you won't get `TLE`. 


* For each point `p`, calculating the distance of `p` with other points and store the distance and its corresponding counts in a map.
* For each point `p`, after getting the map, if the value of count is greater than 1, that means there are at least 2 points which can make a pair with `p`. Since if there are 3 points which can make a pair with `p`, the result is `3 * 2`, that is permutation.


## Code


Python

```python
class Solution(object):
    def numberOfBoomerangs(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        result = 0
        for x1, y1 in points:
            dist_map = {}
            for x2, y2 in points:
                dist = (x1-x2)**2 + (y1-y2)**2
                dist_map[dist] = dist_map.get(dist, 0) + 1
                    
            for dist, count in dist_map.items():
                result += count * (count - 1)

        return result
```


CPP 

```cpp
class Solution {
public:
    int numberOfBoomerangs(vector<pair<int, int>>& points) {
        int result = 0;
        for ( int i = 0; i < points.size(); i ++ ) {
            map<int, int> hashMap;
            for ( int m = 0; m < points.size(); m ++ ) {
                if ( i == m) { continue; }
                
                int dist = pow(points[i].first - points[m].first, 2) + pow(points[i].second - points[m].second, 2);
                map<int, int>::iterator iter = hashMap.find(dist);
                if ( iter == hashMap.end() ) {
                    hashMap.insert(pair<int, int>(dist, 1));
                } else {
                    hashMap[dist] += 1;
                }
            }
            map<int, int>::iterator iter = hashMap.begin();
            while( iter != hashMap.end() ) {
                result += iter->second * (iter->second - 1);
                iter++;
            }
            map<int, int> swapMap;  
            hashMap.swap(swapMap);  
            hashMap.clear();
        }
        return result;
    }
};
```

