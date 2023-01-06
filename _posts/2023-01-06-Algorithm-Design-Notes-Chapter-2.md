---
layout: post
title: 'Algorithm Design Notes: Chapter 2'
---

## Introduction
This is the second chapter in a series of study notes I made reading [my favorite algorithms book](https://www.algorist.com/). In this chapter, we will discuss how to assess algorithm efficiency by introducing essential concepts in time complexity analysis.

## RAM
Time complexity is a measure of how long an algorithm takes to run as a function of the size of the input. However, determining the exact running time of a program on specific hardware would be an extremely tedious task. To this end, a simplified computational model called **Random-Access Machine** (RAM) is used.

RAM is based on the following assumptions:
- *simple operations* (+, -, /, *, if, call, any memory access) take exactly one time step
- loops are **not** *simple operations*

This allows us to disregard uninteresting implementation and architecture details, and to reason about algorithm efficiency in a machine-independent way.

## The Big Oh
We defined time complexity in terms of the input size, but it is easy to show that different inputs of the same size can have different running times.

So do we want the **best**, the **worst**, or perhaps the **average** running time? It is foolish to depend on the best-case. On the other hand, average-case complexity is quite useful in practice, but it can be tricky to obtain and may require domain-specific considerations, and we would probably still want to know what happens in the worst-case scenario. Thus, the most common and reliable is the worst-case complexity analysis.

There are three primary tools to determine to analyze complexity. Assume $f(n)$ is the true complexity function, then:
- $f(n) = O(g(n))$, means that there exists a constant $c$ such that $c \cdot g(n)$ is an upper bound on $f(n)$, i.e. $f(n)$ is always $\leq c \cdot g(n)$, for all $n \geq n_0$
- $f(n) = \Omega(g(n))$, means that there exists a constant $c$ such that $c \cdot g(n)$ is a lower bound on $f(n)$, i.e. $f(n)$ is always $\geq c \cdot g(n)$, for all $n \geq n_0$
- $f(n) = \Theta(g(n))$, means that there exists a constant $c_1$ such that $c_1 \cdot g(n)$ is an upper bound on $f(n)$ and there exists a constant $c_2$ such that $c_2 \cdot g(n)$ is a lower bound on $f(n)$, for all $n \geq n_0$

The most useful of these is the *Big Oh*, that gives us the upper bound. And although sometimes we might overshoot, i.e. the real complexity is significantly lower than our upper bound, it is the best pick for simple algorithms.

From the definitions above, one can notice that we essentially disregard multiplicative constants in our analysis, i.e. given $f(n) = 0.001*n^2$ and $g(n) = 1000*n^2$, $f(n) = O(g(n))$ even though the $g(n)$ values are a million times larger than $f(n)$ values. A direct implication of this is that we can also disregard the lower order terms. Indeed, given $f(n) = n^2 + n$, if we don't care about whether it is $100 * n^2$ or $10000000 * n^2$, why care about $n$?

Thus to obtain an upper bound on your algorithm, you need only follow down the most computationally expensive path.

## Conclusion
What I attempted here is a bite-sized crash into the most essential basics of complexity analysis. Read the respective chapter of the [original source](https://www.algorist.com/) for a much more detailed discussion.