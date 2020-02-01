---
title: Sort value and return its index using C++
date: 2018-11-18 20:40:10
tags: C++
categories: C++
---

Input a vector and returns index after sorting using C++

```C++
template <typename T>
vector<T> sortIndexes(const vector<T> &v, bool ascend) {

    // initialize original index locations
    IntList idx(v.size());
    iota(idx.begin(), idx.end(), 0);

    // sort indexes based on comparing values in v
    sort(idx.begin(), idx.end(), [&v, ascend](size_t i1, size_t i2) {return  ascend ? v[i1] < v[i2] : v[i1] > v[i2];});

    return idx;
}
```

