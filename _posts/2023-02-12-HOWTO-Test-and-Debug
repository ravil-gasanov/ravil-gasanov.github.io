---
layout: post
title: 'HOWTO: Test and Debug'
---

## Defensive Programming
- Document constraints and assumptions
- Design for easy testing (de-couple, abstract)
- Check conditions on inputs / outputs using assertions
- When using Try-Except, catch as specific errors as possible to avoid suppressing buried bugs (can be a headache in e.g. Python)

## Testing
### Strategies
- Intuition (hunt for weaknesses)
- Random (randomized testing provides statistical quality guarantees)
- Boundary cases (e.g. empty input, etc.)
- Black-box (implementation-agnostic tests)
- Glass-box (implementation-aware tests)
- Path-complete (checking every state combination can be exponentially, but you can typically go through all the paths)

### Tips and Tricks
- Create a table of inputs / expected outputs and implement corresponding unit tests
- Test code as soon as it is running
- Make tests as local as possible (i.e. they should pin-point the bug)

## Debugging
The most important factor in effective debugging is being **systematic**.

### When to Print
- Start of a function
- Result of a function
- Parameters
- Binary search the bug
- Hypothesis (intuition-based)

### Ask yourself
- How did I get this result?
- Is the bug part of a family? (if yes, fix everywhere)

### Logic errors
- Pick simplest test that breaks the logic
- Draw a (logic) picture
- Take a break
- Rubber-duck the code

## References and additional sources
[MIT 6.0001 - Lecture 7 - Testing, Debugging, Exceptions, Assertions](https://ocw.mit.edu/courses/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/resources/mit6_0001f16_lec7/)