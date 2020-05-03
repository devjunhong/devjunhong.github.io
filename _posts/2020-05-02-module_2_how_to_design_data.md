---
title: "Module 2 - How to Design Data"
excerpt: "Series of lecture notes, [edX] How to Code: Simple data"
toc: true
toc_sticky: true
published: true

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
