---
layout: post
title: "Sock Matching Puzzle"
author: "Stephen Penrice"
---
<base target="_blank"/>

## Problem Statement
From the FiveThirtyEight website:

"I have 10 pairs of socks in a drawer. Each pair is distinct from another and consists of two matching socks. Alas, I’m negligent when it comes to folding my laundry, and so the socks are not folded into pairs. This morning, fumbling around in the dark, I pull the socks out of the drawer, randomly and one at a time, until I have a matching pair of socks among the ones I’ve removed from the drawer.

On *average*, how many socks will I pull out of the drawer in order to get my first matching pair?

(Note: This is different from asking how many socks I must pull out of the drawer to *guarantee* that I have a matching pair. The answer to *that* question, by the [pigeonhole principle](https://medium.com/cantors-paradise/the-pigeonhole-principle-e4c637940619), is 11 socks. This question is instead asking about the *average*.)

Extra credit: Instead of 10 pairs of socks, what if I have some large number N pairs of socks?"

## Solution
I'll jump straight to the extra credit; the case $N = 10$ can be obtained by plugging in.

The most familiar way to find the average, i.e. the expected value of $X$ (the number of socks drawn), would be to calculate 

$$\sum_{i=1}^{N+1}iP(X=i)$$.

However there is a trick available because of the fact that the number of socks drawn is a positive integer. The sum above is equal to 

$$\sum_{i=0}^{N}P(X>i)$$.

This is because in the second sum $P(X=1)$ is included once (in the $P(X>0)$ term only), $P(X=2)$ is included twice (in the $P(X>0)$ and $P(X>1)$ terms), and so on. This approach is preferable because there is a neat way to express $P(X>i)$.

Of course $P(X>0)=1$, so the following assumes $i>0$. The key idea for finding $P(X>i)$ is that $X>i$ if and only if the first $i$ socks are all different. The number of ways of choosing $i$ distinct socks is $2N(2N-2) \cdots (2N-2(i-1))$ because we have $2N$ choices for the first sock, leaving $2N-2$ choices for the second, and so on. Similarly the total number of ways of choosing $i$ socks sequentially is $2N(2N-1) \cdots (2N-(i-1))$.  So the probability that $X > i$ is 

$$\frac{2N(2N-2) \cdots (2N-2(i-1))}{2N(2N-1) \cdots (2N-(i-1))}=2^i\frac{N!}{(N-i)!}\frac{(2N-i)!}{(2N)!}$$. 

Luckily, this expression is 1 when $i=0$ so we can use it in that case as well. 

Plugging into the equation above gives us an average of 

$$\sum_{i=0}^{N}P(X>i) = \sum_{i=0}^{N} 2^i\frac{N!}{(N-i)!}\frac{(2N-i)!}{(2N)!} = \frac{N!}{(2N)!}\sum_{i=0}^{N}2^i\frac{(2N-i)!}{(N-i)!}$$


The answer for $N=10$ is 5.675464.
