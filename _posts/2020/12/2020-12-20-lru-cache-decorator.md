---
title: "How to speed up your recursive function in Python?"
excerpt: "@lru_cache decorator might help."
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2020/12/recursive.jpg
  image: /assets/images/2020/12/recursive.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  og_image: /assets/images/2020/12/recursive.jpg

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-12-20T08:06:00-05:00
---

# @lru_cache
```python
@lru_cache(None)
def fib(n: int):
    if n < 2:
        return n 
    return fib(n - 1) + fib(n - 2)
```

It's been a while I have seen @lru_cache [decorator](#decorator) in Python. One day, I need to figure out when we use it and how it works. Today is the day. The code in the above calculates n-th the [Fibonacci number](#fibonacci). 

## What is the @lru_cache decorator? 
Decorator to wrap a function with a memoizing callable that saves up to the 'maxsize' most recent calls. It can save time when an expensive or I/O bound function is periodically called with the same arguments. [[3]](#third) It works in the [LRU(Least Recently Used)](#lru) manner. It discards an element that is accessed late. 

The memoizing technique stores every result and reuses it when we call the function with the same arguments. We can frequently face while we are using dynamic programming. 

## How to boost recursive function? 
If we call the recursive function with the same value of arguments, then we can make our algorithm fast. Using the @lru_cache decorator, it is possible to access the old value that has been evaluated. [[3]](#third) Since it will save the return value on the dictionary, it consumes O(1) time to get the value. 

## What is the meaning of None? 
If maxsize is set to None, the LRU feature is disabled and the cache can grow without bound. [[3]](#third)

# Terms 
## <a name="decorator">Decorator</a>
In object-oriented programming, the decorator pattern is a design pattern that allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class. [[1]](#first)

## <a name="fibonacci">Fibonacci number 
Each number is the sum of the two preceding ones, starting from 0 and 1. [[2]](#second)

## <a name="memoizing">Memoizing</a>
In computing, memoization or memoisation is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again. [[4]](#fourth)

## <a name="dp">Dynamic Programming</a>
Dynamic programming is both a mathematical optimization method and a computer programming method. The method was developed by Richard Bellman in the 1950s and has found applications in numerous fields, from aerospace engineering to economics. [[5]](#fifth)

## <a name="lru">LRU(Least Recently Used)</a>
Discards the least recently used items first. This algorithm requires keeping track of what was used when, which is expensive if one wants to make sure the algorithm always discards the least recently used item. [[6]](#sixth)

# Reference
<a name="first">[1]</a> [https://en.wikipedia.org/wiki/Decorator_pattern](https://en.wikipedia.org/wiki/Decorator_pattern)

<a name="second">[2]</a> [https://en.wikipedia.org/wiki/Fibonacci_number](https://en.wikipedia.org/wiki/Fibonacci_number)

<a name="third">[3]</a> [https://docs.python.org/3/library/functools.html#functools.lru_cache](https://docs.python.org/3/library/functools.html#functools.lru_cache)

<a name="fourth">[4]</a>
[https://en.wikipedia.org/wiki/Memoization](https://en.wikipedia.org/wiki/Memoization)

<a name="fifth">[5]</a> [https://en.wikipedia.org/wiki/Dynamic_programming](https://en.wikipedia.org/wiki/Dynamic_programming)

<a name="sixth">[6]</a>
[https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU)](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU))

<span>Photo by <a href="https://unsplash.com/@seimesa?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Mario Mesaglio</a> on <a href="https://unsplash.com/s/photos/recursive?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>