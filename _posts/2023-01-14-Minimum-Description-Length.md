---
layout: post
title: 'Minimum Description Length'
---

## Introduction

Minimum Description Length (MDL) principle is similar to the age-old concept of Occam's razor. Just like Occam's razor, which states that the simplest explanation is often the best, MDL states that the best model is the one that is the shortest, yet still accurately describes the data.

Unlike the Occam's razor, however, MDL is not just a heuristic, but a well-founded mathematical concept with a solid theoretical motivation.

## Kolmogorov Complexity
To understand MDL, it is perhaps best to start by introducing the Kolmogorov Complexity.

Kolmogorov Complexity of an object is defined as the length of the shortest possible program that produces the object.

$$
K(Data) = min\{length(Program)\}
$$

For example, if we had a string "ab", the shortest program would be simply be:

```python
print("ab") 
```

But imagine we have a string "abab..", where "ab" repeats hundreds of times. Now, we can devise a program shorter than storing the whole string explicitly:

```python
for i in range(100):
    print("ab")
```

Now, the problem with Kolmogorov Complexity is that it is not computable, even if we had infinite computational power. 

This is intuitive if you consider the non-computability of the [halting problem](https://en.wikipedia.org/wiki/Halting_problem), which states that it is not possible to determine beforehand whether a program will ever stop or run forever.

Thus if we tried to search through programs in any way, some of them will never terminate and we will never get the result.

## Minimum Description Length

MDL is closely related to the concept of Kolmogorov Complexity.

In MDL, we try to compress the data by using a statistical model. The score is then obtained by encoding the model and residuals.

$$
MDL(M, D) = L(M) + L(D|M)
$$

MDL is computable and sometimes tractable, because specific assumptions are made. These typically include constraining the model space to a specific class and choosing a fixed code to describe the model and data.

## Conclusion
A much more detailed discussion of MDL can be found in the provided sources below.

The practical benefits of choosing simpler models can be relatively obvious, given the computational and sample size limitations. But in fact, it can be shown that even with arbitrarily large amounts of data, simpler models might perform better than complex ones, even if the true model is complex.

## References and additional sources
[A tutorial introduction to the minimum description length principle](https://arxiv.org/pdf/math/0406077.pdf)