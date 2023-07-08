---
layout: post
title: 'What do renting an apartment and finding a parking space have in common?'
---

Both can be formulated as *optimal stopping* problems.

Optimal stopping is concerned with choosing the best time to take a specified action (e.g. rent or park) to maximize a reward (better apartment or parking spot). There are many known solutions for optimal stopping problems with simple assumptions. Below we will discuss a few that can be useful in practice.

# Renting
Have you ever tried to rent an apartment in a city like San Francisco or Berlin? Legend has it the apartment usually goes to the person who can physically force the check on the landlord first. If you do not make a decision right away, the apartment will be gone from the market. For simplicity, let's further assume that you have no knowledge of the market and can only rank the apartments you have seen. What should you do to improve your chances of getting the best apartment you can?

The answer is surprisingly simple - look at the first 37%, and then rent the first one better than the best so far. This will give you a 37% chance of getting the best apartment out of all you had planned to check out. For example, if you planned to visit 100 apartments, then you should look at the first 37 (but not rent) and then rent the first one that is better than all the previous apartments.

# Parking
Let's discuss a different setting. You are driving up a long one-way street and would like to park as close as possible to your final destination. Let's further assume that you have an idea about the parking space occupancy rate on this street. When should you stop looking and park the car?

| Occupancy (%)  | Stop looking at this many spaces away|
|----------------|-----------------|
| 0              | 0               |
| 50             | 1               |
| 75             | 3               |
| 90             | 7               |
| 95             | 14              |
| 99             | 69              |
| 99.9           | 693             |


# Conclusion
This post is inspired by [Algorithms to Live By](https://algorithmstoliveby.com/), which has a more detailed discussion of optimal stopping as well as many other useful algorithms.