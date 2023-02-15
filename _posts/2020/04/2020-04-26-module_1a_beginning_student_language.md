---
title: "Module 1a - Beginning Student Language"
excerpt: "The first module of [edX] How to Code: Simple data"
toc: true
toc_sticky: true
published: true

categories:
    - How to Code
tags:
    - How to Code
    - BSL
    - Software design
last_modified_at: 2020-04-26T08:06:00-05:00
---



## Snippet of Beginning Student Language (BSL)
1. Importance of knowing exactly what I want to make 
2. Break well-chosen pieces of code

Usually, all requirements are quite vague and we have no idea what we want to do at the very beginning. So, it is essential to define what we want to make. In this post, I'm summarizing what I've learned from a course [How to Code: Simple data](https://www.edx.org/course/how-to-code-simple-data). This course is a part of the core computer science course from [OSSU curiculum](https://github.com/ossu/computer-science). The OSSU is Open Source Society University. People build up a curriculum using a free online course. So, this is not by the famous professor but by people. The How to Code course is focusing on designing a program. Instead of learning a new language, a lecturer introduces a simple one; Beginning Student Language(BSL).


## Arithmetic operation
In the BSL, the math operation can be written like this. 

```
(operator operand1 operand2 operand3 operand4)
```

For example, 
```
(+ 3 2)
;5

(/ 12 3)
;4

(sqr 3)
;9

(sqrt 16)
;4

(+ 3 2 2)
;7
```

The 'sqr' is the square operator and 'sqrt' is the square root operator. 


## Evaluation in action 
```
(+ 2 (* 3 4) (- (+ 1 2) 3))
(+ 2 12      (- (+ 1 2) 3))
(+ 2 12      (- 3       3))
(+ 2 12      0)
14
```

In BSL, the first line of code will be reduced by the following formulas. We can observe by walking through from left to right and inside to outside. The above code shows a procedure of evaluation in BSL. 


## String primitives 
```
(string-append "abc" "def" "ghi")
;"abcdefghi"
(string-length "junhong kim")
;11
(substring (string-append "abc" "def" "ghi") 0 4)
;"abcd"
```


## Image evaluation 
```
(require 2htdp/image)

(circle 10 "solid" "red")
(rectangle 30 60 "outline" "blue")
(text "hello" 24 "orange")

(above (circle 10 "solid" "red")
       (circle 20 "solid" "yellow")
       (circle 30 "solid" "green"))

(beside (circle 10 "solid" "red")
       (circle 20 "solid" "yellow")
       (circle 30 "solid" "green"))

(overlay (circle 10 "solid" "red")
       (circle 20 "solid" "yellow")
       (circle 30 "solid" "green"))
```

The above codes produce this result in the same order. The 'require' means importing or loading library functions.

![Image evaluation in BSL](/assets/images/bsl_image_evaluation.png)


## Define constant 
```
(define WIDTH 400)
(define HEIGHT 600)
```

The constant variable doesn't need to be in the capital but it is recommended to use in the capital. It is important to keep a good naming convention for constant variables. 


## Functions 

```
(define (bulb c)
  (circle 40 "solid" c))

(above (bulb "red")
       (bulb "yellow")
       (bulb "green"))
```

Here is how we can define a function using BSL. The first 2 lines define the bulb function with the 'c' parameter. The last 3 lines are calling the bulb function. The function is a key element to break a task into well-chosen pieces of code. 

```
(define (<function_name> <name> ...)
    <expression>)

(function_name parameters|expression)
```


# Boolean 
```
(define WIDTH 100)
(define HEIGHT 100)

(> WIDTH HEIGHT)
;false
(>= WIDTH HEIGHT)
;true
(= 1 2)
;false
(= 1 1)
;true
(> 3 9)
;false

(string=? "foo" "bar")
;false 

(define I1 (rectangle 10 20 "solid" "red"))
(define I2 (rectangle 20 10 "solid" "blue"))
(< (image-width I1)
   (image-width I2))
;true
```
For an equality check is here in BSL, we use one equal sign and for string, we need to 'string' following by equal and question mark(string=?). The last 4 lines that produce true value mean compare the image width of two rectangles. 


# if expression 
```
(if <expression must produce boolean>
    <expression for true case>
    <expression for false case>)

(define I1 (rectangle 10 20 "solid" "red"))
(define I2 (rectangle 20 10 "solid" "blue"))

(if (< (image-width I1)
       (image-height I1))
    "tall"
    "wide")
;"wide"

(if (< (image-width I2)
       (image-height I2))
    "tall"
    "wide")
;"tall"
```

Let's see how if statement looks like in BSL. The above code demonstrates how to write if a statement. 

```
(define I1 (rectangle 10 20 "solid" "red"))
(define I2 (rectangle 20 10 "solid" "blue"))

(and (> (image-height I1) (image-height I2))
     (< (image-width I1) (image-width I2)))

(or (> (image-height I1) (image-height I2))
     (< (image-width I1) (image-width I2)))
```

This is a code to concatenate boolean operation with 'and' and 'or' operators. 


## IDE (DrRacket) and tips

I use DrRacket and I found useful shortcuts to hide interaction area by putting cmd + e. To run the code, hit cmd + r. 