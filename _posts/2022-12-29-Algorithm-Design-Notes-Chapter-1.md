---
layout: post
title: 'Algorithm Design Notes: Chapter 1'
---
## Introduction
This is the first chapter in a series of study notes I made reading [my favorite algorithms book](https://www.algorist.com/). They are not intended (and can't) replace the original material, but can serve as a good refresher or a quick (but not complete) overview to help the reader improve their algorithm design and problem-solving skills.

In this chapter, we will discuss how to formulate the problem, build a solution and reason about its correctness.

## Problem Statement
A well-specified problem includes a complete description of:
- all allowed input
- expected output given input

Take extra care to correctly specify and solve *your problem*, and not some other problem.

## Problem Modelling
Avoid re-inventing the wheel. The most important algorithm design technique is *modelling*.

*Modelling* is formulating the problem in terms of well-studied abstract structures and algorithms.

To give a simple example: calculating the shortest distances between pairs of cities, given a set of roads connecting them - is nothing more than a graph structure + shortest-paths algorithm.

Common structures: permutations, graphs, trees, subsets, points, polygons, strings.

Beware that some problems can be hard to model using standard parts. While certain problems can be modelled several ways, some ways being much better than others.

If you are struggling, a good strategy is to try and relax the problem by constraining the input, and see if you can solve the simpler special case of the original problem.

## Reasoning about correctness
Just because a solution seems reasonable, does not mean it is correct. Or even good.

Thorough mathematical proofs require great care and considerable skill. They are usually not a luxury software engineers can afford at work. However, there is still a lot of value in being able to reason about the correctness.

### Counterexamples
The best way to quickly disprove an idea is to provide a counterexample.

A good counterexample is **verifiable** and **simple**.

Other tips and tricks:
- Think small (consider small cases)
- Think exhaustively (try to cover all base cases)
- Go for a tie
- Go for extremes
- Hunt for weaknesses

### Induction
*A computer scientist is a mathematician, who can only prove things by induction.*

— possibly a paraphrase, can't remember/find the original source

Indeed, most algorithms can be proved by induction due to their incremental or recursive structure. But doing so is rarely straightforward.

Proof by induction consists of two steps:
1. Prove the base case (usually n = 0 or n = 1)
2. Prove the induction step (i.e. if it works for n - 1, it works for n)

In other words, we first prove that the algorithm works for the most elementary case (base case), and then prove that if it worked for *any* previous iteration (n - 1) it works for the current one (n).

Intuitively then - if it works for n = 0, and we prove that if it works for n - 1 then it works for n - it works for n = 1 (because we know n = 0 works), and then by the same logic it works for n = 2, n = 3, and so forth...

The hard part of proving by induction usually comes down to correctly and conveniently formalizing the algorithm and the correctness criteria.

## Conclusion
Follow me on [LinkedIn](https://www.linkedin.com/in/ravilgasanov/) to get notified when the upcoming chapters are published. Starting from Chapter 3, I plan to add a list of *finger exercises* that will help you master a specific concept or technique covered here.

## References and additional sources
[Algorithm Design Manual](https://www.algorist.com/)