---
title: "Module 2 - How to Design Data"
excerpt: "Series of lecture notes, [edX] How to Code: Simple data"
toc: true
toc_sticky: true
published: false

categories:
    - How to Code
tags:
    - How to Code
    - Design data
last_modified_at: 2020-05-02T08:06:00-05:00
---

### Cond operator 
```
(define (aspect-ratio img)
  (cond [Q A]
        [Q A]
        [Q A]))

;[1]
(define (aspect-ratio img)
  (cond [(> (image-height img) (image-width img)) "tall"]
        [(< (image-height img) (image-width img)) "wide"]
        [else "square"]))

;[2]
(define (aspect-ratio img)  
  (if (> (image-height img) (image-width img))
      "tall"
      (if (= (image-height img) (image-width img))
          "square"
          "wide")))
```
When we have more than 2 cases, then we can use the 'Cond' operator. The first one is simplified version of cond operator. Observing the simple one makes sense then the real example. [1] and [2] are the same function but with cond operator and if statement respectively. In the cond expression, each question must produce boolean value.


### Data definition
Data definition describes:
- how to form data of a new type
- how to represent information as data
- how to interpret data as information
- template for operating on data

Data definition simplifies function:
- restricts data consumed
- restricts data produced
- helps generate examples
- provides template


### How to data design recipe 
In this example, we will take steps to build city name data. Since it is a name, we are going to use string data. 
#### Structure definition 
```
; INFORMATION       DATA
; Vancouver         "Vancouver"
; Boston            "Boston"
```

#### Type comment 
```
;; CityName is String
```

#### Interpretation 
```
;; interp. the name of a city
```

#### Examples of the data
```
(define CN1 "Boston")
(define CN2 "Vancouver")
```

#### Templates for a 1 argument function
```
(define (fn-for-city-name cn)
    (... cn)))
```

#### Completed design data
```
;; CityName is String
;; interp. the name of a city

(define CN1 "Boston")
(define CN2 "Vancouver")

#;
(define (fn-for-city-name cn)
    (... cn)))

;; Template rules used:
;; - atomic non-distinct: Image
```


### Combine design function and data 

In the previous [post](https://devjunhong.github.io/how%20to%20code/module_1b_how_to_design_functions/), we take a look how to design a function. Since we work closely with data and function, we need to understand how to do both in terms of using design receipe. When we want to build a function that consumes non-primitive data, we can copy the template we've wrote in design receipe. 

In addition, all the time designing a function and data is independently. It doesn't produce a side-effect when we change input or output forms of data consumed by a function.


### Intervals
Interval represents sequence of integers in a row. In the notation, the square bracket means including and round bracket means excluding. Let's make an example about intervals. 

```
[2, 4]
; 2, 3, 4
(1, 3]
; 2, 3
(3, 6)
; 4, 5
```

Here is the design example of the interval about row seat number from 1 to 32. 
```
;; SeatNumber is Natural [1, 32]
;; interp. the number of seats in the theater
(define S1 1)   ; start
(define S2 10)  ; middle
(define S3 32)  ; end

#;
(define (fn-for-seatnumber sn)
  (... sn))

;; Template rules used:
;; - atomic non-distinct: Natural [1, 32]
```


### Enumeration 
Here is the full design receipe to use enumeration and it represents letter grade. 

```
;; Grade is one of:
;;  - "A"
;;  - "B"
;;  - "C"
;; interp. the grade of a score

;; <examples are redundant for enumerations>
 
#;
(define (fn-for-grade s)
  (cond [(string=? "A" s) (...)]
        [(string=? "B" s) (...)]
        [(string=? "C" s) (...)]))
;; Template rules used:
;;  - one of: 3 cases
;;  - atomic distinct: "A"
;;  - atomic distinct: "B"
;;  - atomic distinct: "C"
```


### Itemization
When we have different subclass type, then we can use the itemization instead of the enumeration. That's the one difference between the enumeration and itemization.

```
;; Countdown is one of:
;;  - false
;;  - Natural[1,10]
;;  - "complete"
;; interp.
;;    false means countdown has not yet started
;;    Natural[1,10] means countdown is running and how many seconds left
;;    "complete" means countdown is over

(define CD1 false)
(define CD2 10)
(define CD3 1)
(define CD4 "complete")

(define (fn-for-countdown c)
  (cond [(false? c) (...)]
        [(and (number? c) (<= 1 c) (<= c 10)) (... c)]
        [else (...)]))

;; Template rules used:
;;  - one of: 3 cases
;;  - atomic distinct: false
;;  - atomic non-distinct: Natural[1, 10]
;;  - atomic distinct: "complete"
```

### Tips 
- '#;': This will comment out following open bracket and close bracket. So in the following example, the right next define statement will be commented out because of '#;'.
```
#;
(define (aspect-ratio img)  
  (if (> (image-height img) (image-width img))
      "tall"
      (if (= (image-height img) (image-width img))
          "square"
          "wide")))
```
