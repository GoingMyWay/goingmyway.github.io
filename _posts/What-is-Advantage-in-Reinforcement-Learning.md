---
title: What is Advantage in Reinforcement Learning?
date: 2018-12-21 14:04:19
tags: Reinforcement Learning
category: Reinforcement Learning
---


In reinforcement learning, an agent behaves according to a stochastic policy $\pi$, the values of the state-action pair $\left (s, a \right )$ and the state $s$ are defined as follows

$$
Q^{\pi}(s, a) = \mathbb{E} [R_t | s_t = s, a_t = a, \pi ],
$$
and 

$$
V^{\pi}(s) = \mathbb{E}_{a \sim \pi(s)} [Q^{\pi}(s, a)]
$$

The former measures the value of choosing a particular action given a state, however the later shows how good it is to be in a particular state $s$, one can easily find that it is the expectation of all actions $a \sim \pi( \cdot )$ under a given state $s$ and a policy $\pi( \cdot )$

The Advantage function can be defined as 

$$
A^{\pi} (s, a) = Q^{\pi} (s, a) - V^{\pi} (s)
$$

Note that $\mathbb{E}_{a \sim \pi(s)} [A^{\pi}(s, a)] = 0$. The advantage function substracts the value of the state from $Q$ function to gain a meatures dipicting the relative significance of curren action $a$. More intuitively, $V$ serves  as a baseline and advantage defines the relative importance of actions, that is to say, a good action can gain a large advantage.

