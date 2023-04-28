---
layout: post
title: 'HOWTO: Code'
---

## Decomposition
Divide code into modules that are *self-contained* and *reusable*. This helps to keep code organized and coherent. Avoid surprises, i.e. put code where others would expect to find it. Can be achieved by using functions, classes, name spaces, code files.

## Abstraction
Abstraction means *showing the what, and not the how*. Abstract if you don't want to remember implementation details, but be careful to provide a clear idea of what the code does.

## Function Design
Each function should do exactly one job. That job should be clearly stated in the name of the function. Short, descriptive, unambiguous, and consistent naming are important in complex programs:
- If the name is too long, it will clutter the code and the reader is more likely to use the wrong function.
- Consistent naming for similar functions allows to understand the behavior of the functions faster. E.g. "get_" prefixes for functions that data elements, etc.

Do not repeat yourself (DRY). Write reusable code once, modify and debug it only in one place. Split your code into general (abstract) functions/classes that you can use as building blocks.

## Object-Oriented Design
Classes are bundles of data and functions (typically called methods in OOP context), often designed to imitate real-world objects. In essence they are just another abstraction tool, so the function design principles apply to classes as well.

There is a lot to be said about Object-Oriented Design, but here are the three corner stones:
- *Encapsulation*: hide implementation details and only expose the necessary functionality through a well-defined interface.
- *Inheritance*: abstract and organize code hierarchically.
- *Polymorphism*: can be implemented in different ways, but the central idea is to enable functions to operate on different data types without changing the interface.

## References and additional sources
[MIT 6.0001 - Lecture 4 - Decomposition, Abstraction, Functions](https://ocw.mit.edu/courses/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/resources/lecture-4-decomposition-abstraction-and-functions/)

[Composing Programs](http://composingprograms.com/)