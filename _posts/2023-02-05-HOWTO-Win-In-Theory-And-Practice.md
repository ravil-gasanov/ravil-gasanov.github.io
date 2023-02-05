---
layout: post
title: 'HOWTO: Win in Theory and Practice'
---

## Introduction
Suppose you become *the most brilliant casino gambler that has ever walked the earth* and discover a strategy that gives you a 51% chance of doubling your bet. Now, if you are familiar with statistics this will sound like great news. If you are not and kind of skeptical, run a simulation with 1,000,000 bets played and look at your net. here's the python code:

```python
import random

LOSE = -1
WIN = 1

WIN_PROB = 0.51
LOSE_PROB = 1 - WIN_PROB

NUMBER_OF_PLAYS = 1000000

def simulation():
    profit = 0

    for i in range(NUMBER_OF_PLAYS):
        outcome = random.choices([LOSE, WIN], weights = [LOSE_PROB, WIN_PROB], k = 1)[0]
        profit += outcome * 250
    
    print(f"Profit: ${profit}")

simulation()
```

Convinced now? Too soon.

## NIL - No Infinite Loan
The fatal flaw in our simulation is the assumption that you can have an unlimited negative profit (i.e. loss), which allows to overcome unlucky streaks, where you would otherwise lose all your money and **stop**. Indeed, even though a large number of plays with a 51% winning chance gives you a serious edge, in the short run, it's very much likely to lose everything. Moreover, if you played infinitely many games with a finite budget - you are bound to hit a unlucky streak that will lose you all your money, so the real world expected profit will be 0. Let's run some simulations to make things concrete.

```python
def fixed_bet(money):
    return 100

def gamble(bet):
    money = 1000
    games = 0

    for i in range(NUMBER_OF_PLAYS):
        if money <= 0:
            break
        outcome = random.choices([LOSE, WIN], weights = [LOSE_PROB, WIN_PROB], k = 1)[0]
        money += outcome * bet(money)

        games += 1

    print(f"Money: ${money}")
    print(f"Games: {games}")

print("Using fixed bet strategy:")
gamble(fixed_bet)
```

What happens now? Losing? Oh no, try starting with more money or decreasing the size of the bet, can you win now?

If you picked a small enough *bet / money* ratio, you might have won, but likely nowhere near as much as in the first naive simulation, unless you have allowed for a ridiculous amount of starting money.

So, the natural question is can you do better than a fixed size bet? Try experimenting with other strategies or jump straight to the theoretically optimal one below.

## Kelly Criterion
John Kelly was an associate of Claude Shannon at Bell Labs, where he built on Shannon's early information theory work to develop what later became known as the Kelly Criterion.

[Kelly Criterion](https://en.wikipedia.org/wiki/Kelly_criterion) is a relatively simple formula that calculates the size of the bet you should make to maximize the rate of return, i.e. win as much money as possible as quickly as possible. Let's try it:

```python
def kelly_bet(money):
    odds = 1 # 1 to 1 odds == doubling bet
    kelly = WIN_PROB - LOSE_PROB / odds

    return kelly * money

print("Using kelly bet:")
gamble(kelly_bet)
```

Congratulations, you have won all the money in the world.

## Conclusion
Now, it is important to note a few things. First, the kelly criterion is very sensitive to how accurately you have estimated the probabilities. Second, your chances of winning must be positive.

So why is no one using this yet, e.g. to invest in stocks or what not? Turns out, people do. In fact, it has been successfully used both in gambling (not recommended) and mainstream investment theory.