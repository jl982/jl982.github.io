---
layout: post
title: Solving probability problem with code
date: 2021-02-23
tags: software
---

## The Problem
Last weekend, as I was casually browsing the [CS:GO subreddit](https://www.reddit.com/r/GlobalOffensive) for any news related to the game, I found myself in a staring contest with a [math problem](https://www.reddit.com/r/GlobalOffensive/comments/lorda5/a_csgo_math_question_appear_in_a_practice_math/go7e3z3):

> Question: A player is holding a Desert Eagle and facing an enemy. Each shot he fires has 50% chance of hitting the enemy. If the shot is accurate, there's also a 20% chance of headshot which will kill the target immediately, otherwise, it requires 3 shots to take down the enemy. What's the probability of the player to take down the enemy in 7 shots?

"Interesting," I thought to myself, trying to jog my memory of probability theory. But soon, it dawned on me that perhaps the mathematical solution won't come very easily. And soon after that, it became a matter of pride to be able to solve the problem through some means. So I turned to what I'm more familiar with these days: coding.

## Monte Carlo method
One nice thing about probability problems is that even if you don't know the exact answer, you can always approximate it by running experiments. This is known as the [Monte Carlo method](https://en.wikipedia.org/wiki/Monte_Carlo_method).

I opened up a text editor, and quickly translated the problem to JavaScript (mostly because it is the easiest to work with, as I can run JavaScript directly in my browser's developer console):

~~~javascript
// runs one round of simulation: true if dead in 7 shots
function sim() {
  var body = 0;
  for (var i = 0; i < 7; i++) {
    if (Math.random() < 0.5) {
      if (Math.random() < 0.2) return true;
      else body += 1;
      if (body == 3) return true;
    }
  }
  return false;
}

// runs many simulations and keeps tally
function run(total) {
  var dead = 0;
  for (var i = 0; i < total; i++) {
    if (sim()) dead += 1;
  }
  return dead * 1.0 / total;
}

run(10000000); // returns 0.8434493
~~~

Not bad for a few minutes of coding. Elated, I went to look for an answer that's close to 84.34% and found... none?

<figure>
<img src="https://i.redd.it/40vudn7h4si61.jpg"/>
<figcaption markdown=span>The original question (in Vietnamese) did not have the correct answer</figcaption>
</figure>

But false alarm. Based on the comments in the Reddit post, the consensus is that the provided answer [missed a case](https://www.reddit.com/r/GlobalOffensive/comments/lorda5/a_csgo_math_question_appear_in_a_practice_math/go8a3ok/), and that 84.34% is the right answer. Phew.

## Exact solution
Several other people also coded Monte Carlo simulations, and it was interesting to compare our algorithms. What really caught my eyes though, was [this solution](https://www.reddit.com/r/GlobalOffensive/comments/lorda5/a_csgo_math_question_appear_in_a_practice_math/go7rlr2), which instead uses recursion to find the exact probability (slightly edited for readability):
~~~python
def f(shots, hp):
  if hp == 0:
    return 1
  elif shots == 0:
    return 0
  # 10% headshot, 40% body shot, 50% miss
  return 0.1 * f(shots - 1, 0) + \
         0.4 * f(shots - 1, hp - 1) + \
         0.5 * f(shots - 1, hp)

print(f(7, 3)) # returns 0.8434375
~~~

It's quite brilliant. The base cases are when `hp` or `shots` is 0; otherwise, the logic recursively progresses toward one of the base cases.

The mathematical solution turns out to be simple too. [Here's one approach](https://www.reddit.com/r/GlobalOffensive/comments/lorda5/a_csgo_math_question_appear_in_a_practice_math/go8uvk2) that calculates the probability of surviving, then subtracts it from 1 to arrive at the answer:
```
P(dies) = 1 - P(survives)
P(survives) = P(no hits) + P(1 hit, no headshots) + P(2 hits, no headshots)
P(no hits) = 0.5^7 ~ 0.78%
P(1 hit, no headshots) = 7C1 * 0.5^7 * 0.8 ~ 4.38%
P(2 hits, no headshots) = 7C2 * 0.5^7 * 0.8^2 ~ 10.5%
So P(dies) ~ 84.34%
```

## Discussion
Learning fundamental concepts such as math and probability theory is obvious important. However, using code, sometimes it's good enough to let computer do most of the hard work.

Discuss this post on [HN](https://news.ycombinator.com/item?id=26242445).
