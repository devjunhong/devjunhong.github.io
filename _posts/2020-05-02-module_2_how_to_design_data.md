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
