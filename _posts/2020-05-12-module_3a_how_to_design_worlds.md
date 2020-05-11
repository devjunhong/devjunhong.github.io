---
title: "Module 3a - How to Design Worlds"
excerpt: "Series of lecture notes, [edX] How to Code: Simple data"
toc: true
toc_sticky: true
published: true

categories:
    - How to Code
tags:
    - How to Code
    - Design
last_modified_at: 2020-05-11T08:06:00-05:00
---

### big-bang

So far, we've understood how to use design reciepe in terms of defining a [function](https://devjunhong.github.io/how%20to%20code/module_1b_how_to_design_functions/) or [data](https://devjunhong.github.io/how%20to%20code/module_2_how_to_design_data/). In this week, we are going to work with interactive program that can produce graphical result by entering space or enter key. 

Using the big-bang function is the one of way to create interactive program. We will pass some inputs to big-bang function and it will produce a world just like how the space was originated. Since we can pass various types of input data to big-bang function, we call it "polymorphism".

```
(big-bang 0
            (on-tick next-cat)
            (to-draw render-cat))
```

0 means the initial state. 'next-cat' is a function that produces a next state. 'render-cat' is a function that consumes the produced state by 'next-cat'. The below figure cleary represents how the big-bang function works. 

![big-bang function](/assets/images/big_bang_works.png)