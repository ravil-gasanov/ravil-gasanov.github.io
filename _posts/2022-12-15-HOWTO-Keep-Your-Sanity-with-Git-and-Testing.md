---
layout: post
title: 'HOWTO: Keep Your Sanity with Git and Testing'
---

## 1. Keep it small
Keep your commits small. This has several benefits:
- easier for other people to review and accept your pull requests

- easier to keep track of concrete changes and roll back when necessary
- forces you to write cleaner code, as you have to break up complex methods in shorter abstract ones
- good quality unit tests become a natural part of the process

## 2. 100% coverage is a good start
Make sure every part of the project code is covered by tests, at the very least you can avoid most trivial errors. Which is especially important when you are working with languages like Python and do not want to get annoying runtime surprizes, like syntax errors.

But to properly test your software, you will have to go beyond 100% coverage with unit tests and make heavy use of functional and integration tests.

*''My dear, here we must run as fast as we can, just to stay in place. And if you wish to go anywhere you must run twice as fast as that.''*

— Lewis Carroll, Alice in Wonderland


## 3. The strategic kind of lazy
There will come a point, when you will (want to) skip testing some part of the code. Because it is difficult to test or you don't have time or some other excuse. 

You will inevitably regret it, of course, because it will lead to overall more work. But that's the future you's problem, right?

A simple trick to add some resistance to such behavior is to introduce pre-commit hooks, that will make sure all your tests are green and you have 100% coverage before allowing the commit.

![pre-commit]({{ site.baseurl }}/images/pre-commit-hooks.png "Pre-commit hooks")

## References and additional sources
[MIT 6.0001 - Lecture 7 - Testing, Debugging, Exceptions, Assertions](https://ocw.mit.edu/courses/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/resources/mit6_0001f16_lec7/)

[30 best practices for software development and testing](https://opensource.com/article/17/5/30-best-practices-software-development-and-testing)