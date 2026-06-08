+++
title = "Calculating π from random numbers"
date = "2026-06-08"
description = "Using basic profiling tools to optimise a simple go program."
tags = [
    "go",
    "linux",
    "pprof"
]
+++

Matt Parker of [Stand-up Maths](https://www.youtube.com/@standupmaths) fame has a yearly series where he tries to calculate π by various,(sometimes ridiculous) techniques. [This](https://www.youtube.com/watch?v=lmgCgzjlWO4) is a personal favourite, where he uses Avogadro's number and it was more accurate than I would have expected.
The rest of this post is based on [this](https://www.youtube.com/watch?v=RZBhSi_PwHU) video from 2017 and basically boils down to the fact that the probability of two random numbers being co-prime is 6/ π^2.  This comes from a famous problem in mathematical analysis called the [Basel Problem](https://en.wikipedia.org/wiki/Basel_problem) and was solved by Euler

---
I have been using a lot of Claude at work and am trying to step away from it for my personal coding. After a lot of bike-shedding in getting my [vim-go](https://github.com/fatih/vim-go/) configured just right, I decided to try this out. The core problem is very simple and just involves calculating the GCD of 2 numbers and doing that for a lot of numbers to estimate the probability. I wanted to use some of the standard profiling tools to visualise the performance and optimise some of the low hanging fruit.There are probably smarter ways of calculating GCD ( or checking if numbers are co-prime), but that is not point of this post.
 
I ran the benchmarking tests on a Linux environment powered by an AMD Ryzen 7 5800H processor (8 cores, 16 threads)


## Baseline

I am generating numbers in the range 1 - 1 billion and counting the results from 1 billion pairs.

The [first](https://github.com/bobbyphilip/go-sandbox/commit/a4b1dcdff0d30013c13b987eeb4ad07f26981314) naive implementation doesnt try to do anything clever and just hammers away at the problem.
![image](images/260608-baseline.jpg)

and 
![image](images/260608/baseline.jpg)

Looks like we have π, if we dont look very hard.  It took about a minute to run, wall time and cpu time are pretty much the same.

---


