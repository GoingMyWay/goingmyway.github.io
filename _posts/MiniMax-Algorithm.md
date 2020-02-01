---
title: MiniMax Algorithm
date: 2018-08-14 18:47:06
tags: Algorithm
categories: Algorithm
---

The Key idea for MiniMax Algorithm is the best action of a player against the other player's action.


here is the pesuode code

```python
def MiniMax(state):
    vs = []
    for next_state in next_states(state):
        vs.append(Max(next_state))
    return max(vs)

def Max(state):
    if terminal(state):
       return utility(state)
    vs = []
    for next_state in next_states(state):
        vs.append(Min(next_state))
    return max(vs)

def Min(state):
    if terminal(state):
        return utility(state)
    vs = []
    for next_state in next_states(state):
        vs.append(Max(next_state))
    return min(vs)
```

Reference

* https://www.youtube.com/watch?v=6ELUvkSkCts
* https://www.youtube.com/watch?v=zp3VMe0Jpf8
