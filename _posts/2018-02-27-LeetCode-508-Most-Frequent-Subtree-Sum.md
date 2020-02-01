---
title: LeetCode 508. Most Frequent Subtree Sum
date: 2018-02-27 15:33:00
tags: LeetCode
categories: LeetCode
---

Hi again, happy Chinese New Year, it is a long since that last post. Here is a new LeetCode question on HashTable and Tree, here we go.

## Question

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

**Examples 1**
Input:

  5
 /  \
2   -3
return [2, -3, 4], since all the values happen only once, return all of them in any order.

**Examples 2**
Input:

  5
 /  \
2   -5
return [2], since 2 happens twice, however -5 only occur once.
**Note:** You may assume the sum of values in any subtree is in the range of 32-bit signed integer.

## Solution

You can solve this problem in 3 steps

* step 1

  For each node,visit the node and nodes of its subtrees and add values of each node including itself and return the sum;


* step 2

  create a map to store the value sum and its counts.

* step 3

  return the result.


And there is a better solution using poster order visiting method from down to top. As you can see in the code.


## Code


```cpp
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    vector<int> findFrequentTreeSum(TreeNode* root) {
        unordered_map<int, int> hashMap;
        vector<int> vec, result;
        
        if ( NULL == root ) return result;
        visit(root, hashMap);
        
        for ( auto it: hashMap ) vec.push_back(it.second);
        int maxCount = *max_element(vec.begin(), vec.end());
        
        for ( auto it: hashMap ) {
            if ( maxCount == it.second ) result.push_back(it.first);
        }
        return result;
    }
    
    void visit(TreeNode * node, unordered_map<int, int> & Map) {
        if ( NULL != node ) {
            int res = nodeSum(node);
            if ( Map.count(res) ) Map[res] += 1;
            else Map[res] = 1;
            
            visit(node->left, Map);
            visit(node->right, Map);
        }
    }
    
    int nodeSum(TreeNode * node) {
        if ( NULL == node ) {
            return 0;
        } else {
            return node->val + nodeSum(node->left) + nodeSum(node->right);
        }
    }
};

class Solution2 {
public:
    vector<int> findFrequentTreeSum(TreeNode* root) {
        unordered_map<int, int> hashMap;
        vector<int> vec, result;
        int maxCount = 0;
        
        nodeSum(root, hashMap, maxCount);
        for ( auto it: hashMap ) {
            if ( maxCount == it.second ) result.push_back(it.first);
        }
        return result;
    }
    
    int nodeSum(TreeNode * node, unordered_map<int, int> & Map, int & cnt) {
        if ( NULL == node ) {
            return 0;
        } else {
            int res = nodeSum(node->left, Map, cnt) + nodeSum(node->right, Map, cnt) + node->val;
            cnt = max(cnt, ++Map[res]);
            return res;
        }
    }
};
```
