---
title: "Module 1b - How to Design Functions"
excerpt: "Series of lecture, [edX] How to Code: Simple data"
toc: true
toc_sticky: true
published: true

categories:
    - How to Code
tags:
    - How to Code
    - Design Functions
last_modified_at: 2020-04-26T08:06:00-05:00
---

## How to design functions(HtDF) 
There are exact 5 steps to create functions. It feels like me to develop in TDD passion. As the lecturer said, for building a simple function, it feels like overkill. However, it is helpful to keep following the codebase. 

1. Signature, purpose, and stub.
2. Define examples, wrap each in check-expect.
3. Template and inventory.
4. Code the function body.
5. Test and debug until correct

Let's suppose that we are creating a function that produces twice the given number and take the steps to design a function.


### Signature 
The signature declares a type of data function consumes and produces. (for example, primitive types are Number, Integer, Natural, String Image, and Boolean.)
```
Type ... -> Type
;; Number -> Number
```


### Purpose 
The purpose is a **1 line** description of what the function produces in terms of what it consumes. At the very beginning, it could be cumbersome. When it does, we need to rewrite it in 1 line of the sentence. 
```
;; produce 2 times the given number
```


### Stub
The stub is a function definition that 
* has a correct function name 
* has the correct number of parameters
* produces dummy result of the correct type 

And this will be commented out when we build a template. 
```
(define (double n) 0)
```


### Example 
Examples help us understand what function must do. Multiple examples to illustrate behavior. Wrapping in check-expect means they will also serve as unit tests for the completed function.
```
(check-expect (double 3) 6)
(check-expect (double 4.2) 8.4)
```


### Template
The body of the template is the outline of the function. Before starting to write a code body, it will be commented out or deleted. 
```
(define (double n)
    (... n))
```


### Code body 
Each step helps the very next step in the design recipe. The very previous one help the next one. 


### Debugging 
We inevitably face when designed function not working properly. In that case, we can walk through the design steps so that we can find mismatches from the given purpose, signature, or examples. With this approach, I think I can find a simple bug or tracking the bug where I missed it. Since it does have commented block about the purpose of function, I can grab my previous code very quickly and easily. 


### Rules 
- A function that produces boolean value should use ? in the ends of its name 
- When we write a purpose of the function in case of returning boolean, we need to specify what the true value means.