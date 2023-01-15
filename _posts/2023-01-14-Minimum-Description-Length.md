---
layout: post
title: 'Minimum Description Length'
---

## Introduction

Minimum Description Length (MDL) principle is similar to the age-old concept of Occam's razor. Just like Occam's razor, which states that the simplest explanation is often the best, MDL states that the best model is the simplest one, that still accurately describes the data.

Unlike the Occam's razor, MDL is not just a heuristic, but a well-founded mathematical concept with a solid theoretical motivation.

## Kolmogorov Complexity
To explain MDL, it is perhaps best to start with Kolmogorov Complexity.

Kolmogorov Complexity of an object is defined as the length of the shortest possible program that produces the object.

$$
K(Data) = min\{length(Program)\}
$$

For example, if we had a string "ab", the shortest program would be simply be:

```python
print("ab") 
```

But imagine if we had a string "abab..", where "ab" repeats hundreds of times. Now, we can devise a program shorter than storing the whole string explicitly:

```python
for i in range(100):
    print("ab")
```

## Minimum Description Length

Now, the problem with Kolmogorov Complexity is that it is not computable, even if we had infinite computational power. This is intuitive if you consider the non-computability of the [halting problem](https://en.wikipedia.org/wiki/Halting_problem), which states that it is not possible to determine beforehand whether a program will ever stop or run forever. Thus if we tried to search through programs in any way, some of them will never terminate and we will never get the result.

In contrast, Minimum Description Length is obtained by encoding a statistical model and the data given the model.

$$
MDL(M, D) = L(M) + L(D|M)
$$

MDL is computable, because specific assumptions are made. These typically include constraining the model space to a specific class and choosing a fixed code to describe the model and data.

## Conclusion
A much more detailed discussion of MDL can be found in [this tutorial](https://arxiv.org/pdf/math/0406077.pdf).

The practical benefits of choosing simpler models can be relatively obvious, given the computational and sample size limitations. But in fact, it can be shown that even with arbitrarily large amounts of data, simpler models might perform better than complex ones, even if the true model is complex.