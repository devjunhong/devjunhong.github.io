---
title: "List, Dictionary, and Set Comprehensions"
excerpt: "To make readable code"
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-03-02T08:06:00-05:00
---

## Python Comprehensions 

```python
list(map(FahrenheitToCelsius, [32, 65, 104, 212])) # [1]

[(t*9/5) + 32 for t in [32, 65, 104, 212]] # [2]
```

What is the comprehension? In the above example, [1] and [2] are the same. This is a Python language construct. So that understanding [1] and [2] are the same, and it means we can point readability. If we think [2] is more readable then we can use it. Before writing readable code, we need to understand what's the same and different. It feels like understanding a synonym in the linguistics. 


## List comprehensions

```python
def demo():
    evens = [2, 4, 6, 8, 10]
    odds = [1, 3, 5, 7, 9]

    evenSquared = list(map(lambda e: e**2, 
    filter(lambda e: 4 < e < 10, evens))) # [1]
    print(evenSquared)
    # [36, 64]

    evenSquared = [e ** 2 for e in evens]
    print(evenSquared)
    # [4, 16, 36, 64, 100]

    oddSquared = [o ** 2 for o in odds if 3 <= o < 9] # [2]
    print(oddSquared)
    # [9, 25, 49]


demo()
```

Using the list comprehension, we can rewrite [1] into [2]. And, [2] seems way better readable then [1]. 

## Dictionary comprehensions
```python
def demo():
    ctemps = [0, 12, 34, 100]

    tempDict = {t: (t * 9 / 5) + 32 for t in ctemps 
    if t < 100} # [1]
    print(tempDict)
    # {0: 32.0, 12: 53.6, 34: 93.2}
    print(tempDict[12])
    # 53.6

    team1 = {"Jones": 24, "Jameson": 18, 
    "Smith": 58, "Burns": 7}
    team2 = {"White": 12, "Macke": 88, "Perce": 4}

    newTeam = {k: v for team in (team1, team2) 
    for k, v in team.items()} # [2]
    print(newTeam)
    # {'Jones': 24, 'Jameson': 18, 'Smith': 58, 
    # 'Burns': 7, 'White': 12, 'Macke': 88, 'Perce': 4}


demo()
```

[1] is the basic example to create a dictionary with comprehension and [2] is a complex example to create one. In [2], we want to merge two dictionaries into one. When we use comprehension more than 2 times, it will harm readability. So, we need to restrict the use of comprehension techniques no more than two times. 

## Set comprehension
```python 

def demo():
    ctemps = [5, 10, 12, 14, 10, 23, 41, 14, 14]

    ftemps1 = [(t * 9 / 5) + 32 for t in ctemps] # [1]
    ftemps2 = {(t * 9 / 5) + 32 for t in ctemps} # [2]
    print(ftemps1)
    # [41.0, 50.0, 53.6, 57.2, 50.0, 
    # 73.4, 105.8, 57.2, 57.2] 
    print(ftemps2)
    # {73.4, 41.0, 105.8, 50.0, 53.6, 57.2}

    stemp = "The quick brown fox jumped over the lazy dog"
    chars = {c.upper() for c in stemp 
    if not c.isspace()} # [3]
    print(chars)
    # {'E', 'X', 'W', 'N', 'P', 'T', 'B', 'Z', 'A', 
    # 'M', 'G', 'O', 'C', 'V', 'Q', 'J', 'L', 'Y', 
    # 'K', 'H', 'R', 'D', 'I', 'F', 'U'}


demo()
```

In [1] and [2], these show a difference between the list and the set. In the output prints, we can observe the ftemps1 has a number of items than ftemps2. In the set, duplicates are not allowed. If we want to count unique characters in the string just like in [3], we can use the set.