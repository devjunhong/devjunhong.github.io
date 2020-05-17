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


### How to design worlds
Here, I guess right title will be how to design using the big-bang function. Anyway, I think it's important to follow the design receipe cause it shows cristal clear way to think like a programmer.


#### Domain Analysis
The first part is the domain analysis. By sketching 2 or 3 scenarios, we can observe how the interactive program works with inputs and outputs. According to the scenarios, we need to identify what're the constants and variables in the program. 

#### Build actual program 
The last part is building an actual program with how to design receipe for [function](https://devjunhong.github.io/how%20to%20code/module_1b_how_to_design_functions/) and [data](https://devjunhong.github.io/how%20to%20code/module_2_how_to_design_data/). Surprisingly, it does possible to focus on one thing at each step. In the lecture, it is possible to follow each specific elaborated step one by one. In addition, during the steps, it gives big advise about being easy to change for program is one of the most import properties. 


### Modification 
A program that is used by people need to be well structured for updating issue. Clients always ask for better performance or new design. In terms of updating the software, try to stick with the idea; how to design worlds. 