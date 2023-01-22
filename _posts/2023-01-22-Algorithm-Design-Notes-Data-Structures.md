---
layout: post
title: 'Algorithm Design Notes: Data Structures'
---

## Introduction
This is the third chapter in a series of study notes I made reading [my favorite algorithms book](https://www.algorist.com/). In this chapter, we will discuss essential data structures, their place in algorithm design and important concepts underlying their efficiency.

Many real world problems are modelled naturally by standard data structures like *priority queues* or *dictionaries*. Knowing your way around data structures has the following advantages (sorted by the depth of knowledge required):

- Freely available, highly optimized implementations that can be used as black boxes
- Understanding the trade-offs between different data structures and implementations
- Exploiting existing ideas to build efficient custom solutions

## Contiguous vs Linked
Data structures can be divided into two fundamental categories: *contiguous* and *linked*.
- *Contiguous* structures are allocated in single chunks of memory (e.g. arrays, heaps, hash tables).
- *Linked* structures are allocated in distinct chunks of memory linked by [pointers](https://en.wikipedia.org/wiki/Pointer_(computer_programming)) (e.g. lists, trees, graph adjacency lists).

The contiguous structures provide more efficient random access, but require you to know how much memory you will need in advance. Linked structures are more flexible, but have the cost of storing and operating with pointers. Linked structures are more economical, however, when the data objects are significantly larger than the pointers, since we only use memory as needed and manipulate pointers instead of the objects themselves (imagine moving around gigabyte-sized elements when sorting an array).

| Data Structure      | Insertion  | Deletion   | Search     | Access    |
|---------------------|------------|------------|------------|-----------|
| Array               | O(n)       | O(n)       | O(n)       | O(1)      |
| Linked List         | O(1)       | O(1)       | O(n)       | O(n)      |

## Trade-offs
[The book](https://www.algorist.com/) teaches the nuances of implementation trade-offs by making the student work through examples. Here I will only give you one example, to illustrate the point.

Suppose you want to implement a Priority Queue. You need three basic operations: *insert*, *min*, *delete-min*. Let us now compare two implementations, where you build on top of an unsorted and a sorted array respectively:

| Data Structure      | Insertion  | Min | Delete-min|
|---------------------|------------|------------|------------|
| PQ (unsorted array) | O(1) | O(n) | O(n) |
| PQ (sorted array) | O(n) | O(1) | O(1) |

The above assumes that we have enough memory allocated to the arrays. Can you see why (in the worst case) it takes linear time to insert an element into a sorted array? Or why it only takes constant time to delete an element?

## Conclusion
As usual, read [the book]((https://www.algorist.com/)) (or a book) for a much fuller discussion. I have found particularly interesting the following parts of the chapter:
- Exercises on implementation trade-offs
- Binary Search Trees
- Hashing and its applications

The book also contains a catalogue of data structures in chapter 12. 