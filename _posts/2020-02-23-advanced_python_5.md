---
title: "Basic Collections, DefaultDict, Counters, OrderedDict, and Deque"
excerpt: "collections module"
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-02-23T08:06:00-05:00
---

## Basic Collections 
In Python, we can find useful built-in collections. When we import collections, we have more. In the code example, we will see what're benefits when we use named tuple. 

* list: mutable sequence of values
* tuple: immutable, fixed sequence of values 
* set: immutable, Sequence of distinct values
* dictionary: mutable, collection of key-value pairs

When we use 'import collections', we can find these. 

* namedtuple: tuple with named fields 
* OrderedDict, defaultdict: Dictionaries with special properties
* Counter: Counts distinct values
* deque: Double-ended list object

```python
import collections


def demo():
    Point = collections.namedtuple("Point", "x y")
    p1 = Point(10, 20)
    p2 = Point(30, 40)
    print(p1, p2)
    # Point(x=10, y=20) Point(x=30, y=40)
    print(p1.x, p2.y)
    # 10 40

    p1._replace(x = 100)
    print(p1)
    # Point(x=10, y=20)

    p1 = p1._replace(x = 100)
    print(p1)
    # Point(x=100, y=20)


demo()
```
The named tuple looks more readable and it is immutable as we can see from the last two examples. Instead of referencing an index that has no meaning, we can use the exact name of the element. 


## DefaultDict 
```python
from collections import defaultdict


def demo():
    fruits = ['apple', 'pear', 'orange', 'banana',
    'apple', 'grape', 'banana', 'banana']
    
    fruitCounter = defaultdict(int) 

    for fruit in fruits:
        fruitCounter[fruit] += 1

    for (k, v) in fruitCounter.items():
        print(k + ": " + str(v))

    # apple: 2
    # pear: 1
    # orange: 1
    # banana: 3
    # grape: 1


demo()
```
The DefaultDict will initialize a default value for unseen keys and it's a factory creator. We can pass any object when we create the object. If we don't use the default dictionary object, we need to use the dictionary object and add a check code for a key. The DefaultDict object can reduce the checking code. If we don't know the initial value, then we have to use the dictionary object. 

## Counters
```python
from collections import Counter


def demo():
    class1 = ["Bob", "Becky", "Chad", "Darcy", "Frank", 
              "Hannah", "Kevin", "James", "James",
              "Mealnie", "Penny", "Steve"]
    class2 = ["Bill", "Barry", "Cindy", "Debbie", 
              "Frank", "Gabby", "Kelly", "James",
              "Joe", "Sam", "Tara", "Ziggy"]

    c1 = Counter(class1)
    c2 = Counter(class2)

    print(c1["James"])
    # 2

    # summation of all numbers
    print(sum(c1.values()), " in nums1")
    # 12

    # add up the counter
    c1.update(class2)
    print(sum(c1.values()), " in nums1")
    # 24

    # print out top most common item in the counter
    print(c1.most_common(3))
    # [('James', 3), ('Frank', 2), ('Bob', 1)]
    
    # separate 
    c1.subtract(class2)
    print(c1.most_common(3))
    # [('James', 2), ('Bob', 1), ('Becky', 1)]

    # intersection
    print(c1 & c2) 
    # Counter({'Frank': 1, 'James': 1})


demo()
```
I think this is one most convenient for a data scientist who handles tons of data. A Counter object is a dictionary object that counts how many times the same key appeared in the given list. When we have to draw a distribution of data such as a histogram, the Counter will perfect fit. The above example is quite simple but powerful. I have lots of tasks like this, so I want to use the Counter object aggressively. 


## OrderedDict
```python
from collections import OrderedDict


def demo():
    sportTemas = [("Royals", (18, 12)), ("Rockets", (24, 6)),
                ("Cardinals", (20, 10)), ("Dragons", (22, 8)),
                ("Kings", (15, 15)), ("Chargers", (20, 10)),
                ("Jets", (16, 14)), ("Warriors", (25, 5))]

    sortedTeams = sorted(sportTemas, key=lambda t: t[1][0], 
    reverse=True)

    teams = OrderedDict(sortedTeams)
    print(teams)
    # OrderedDict([('Warriors', (25, 5)), 
    # ('Rockets', (24, 6)), 
    # ('Dragons', (22, 8)), ('Cardinals', (20, 10)), 
    # ('Chargers', (20, 10)), ('Royals', (18, 12)), 
    # ('Jets', (16, 14)), ('Kings', (15, 15))])

    tm, wl = teams.popitem(False)
    print("Top team: ", tm, wl) 
    # Top team:  Warriors (25, 5)

    for i, team in enumerate(teams, start=1):
        print(i, team)
        # 1 Rockets
        # 2 Dragons
        # 3 Cardinals
        # 4 Chargers
        if i == 4:
            break 

    a = OrderedDict({"a": 1, "b": 2, "c": 3})
    b = OrderedDict({"a": 1, "b": 2, "c": 3})
    print("Equality test: " , a == b)
    # [1] Equality test:  True

    c = OrderedDict({"a": 1, "c": 3, "b": 2})
    print("Equality test: " , a == c)
    # [2] Equality test:  False

    a = {"a": 1, "b": 2, "c": 3}
    c = {"a": 1, "c": 3, "b": 2}
    print("Equality test: " , a == c)
    # [3] Equality test:  True


demo()
```
OrderedDict keeps order and it checks equality with the order. [1], [2], and [3] examples show the equality checks. That's the one thing different from the Dictionary object. If we think the order of object then it is better to use the OrderedDict.


## Deque 
```python
import string

from collections import deque


def demo():
    d = deque(string.ascii_lowercase)

    print("Item count: ", str(len(d)))
    # Item count:  26

    for elem in d: 
        print(elem.upper(), end=",")
        # A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,
        # Q,R,S,T,U,V,W,X,Y,Z,

    d.pop()
    d.popleft()
    d.append(2)
    d.appendleft(1)
    print(d)
    # deque([1, 'b', 'c', 'd', 'e', 'f', 'g', 
    # 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 
    # 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 
    # 'x', 'y', 2])

    print(d)
    # deque([1, 'b', 'c', 'd', 'e', 'f', 'g', 
    # 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 
    # 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 
    # 'x', 'y', 2])
    d.rotate(10)
    print(d)
    # deque(['q', 'r', 's', 't', 'u', 'v', 'w', 
    # 'x', 'y', 2, 1, 'b', 'c', 'd', 'e', 'f', 
    # 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 
    # 'o', 'p'])

demo()
```
* Double-ended queue


The deque is a double-ended queue. It can pop an item from left and right and also push an item to both ends. We can use 'pop', 'popleft', 'append', and appendleft functions to do that. We can also use for rotating the elements which pop the rightmost item and append it to left in a cyclic fashion. I used it a lot when I practice coding interview problems since it can be used in both ways; stack and queue.