---
title: "Handy built in functions"
excerpt: "Useful built in functions; any, all, min, transforms, and itertools."
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-02-16T08:06:00-05:00
---

## any, all, min, max, and sum 
```python
def built_in_operations():
    list1 = [1, 2, 0, 3, 4, 5]
    print(any(list1)) # True
    print(all(list1)) # False, because of the 0
    print(min(list1)) # 0
    print(max(list1)) # 5
    print(sum(list1)) # 15


build_in_operations()
```
* any: if more than 1 thing is True, then return True 
* all: True when all items in list are True 
* min
* max
* sum

In Python, we can find many built-in methods. In particular, within the list object, those are useful when we have to handle data; any, all, min, max, and sum. When I try to practice competitive programming or coding interview, I avoid to use them. It seems for me using those built-in functions cannot verify my logics. 

## iteration 
```python
def show_iteration(): 
    digits = [1, 2, 3, 4, 5]
    digitsEn = ['one', 'two', 'three', 'four', 'five']

    # using the iter function
    i = iter(digits)
    print(next(i)) # 1
    print(next(i)) # 2

    # read a file line by line 
    with open('_test/testfile.txt', 'r') as fp:
        for line in iter(fp.readline, ''):
            # print next line until meet '' (sentinel)
            print(line) 

    # looping over collection 
    for d in digits:
        print(d)
    # 1
    # 2
    # 3
    # 4
    # 5

    # index 
    for i in range(len(digits)):
        print(i + 1, digits[i])
    # 1 1
    # 2 2 
    # 3 3
    # 4 4
    # 5 5

    # enumerate
    for i, d in enumerate(digits):
        print(i, d)
    # 0 1
    # 1 2
    # 2 3
    # 3 4
    # 4 5

    # zip
    for m in zip(digits, digitsEn):
        print(m)
    # (1, one)
    # (2, two)
    # (3, three)
    # (4, four)
    # (5, five)

    # zip and enumerate
    for i, m in enumerate(zip(digits, digitsEn), start=1):
        print(i, m[0], ' = ', m[1])
    # 1 1 = one
    # 2 2 = two
    # 3 3 = three
    # 4 4 = four
    # 5 5 = five
    

show_iteration()
```
Iteration is one of the frequent logic we can find in any code. When you find a CSV file with tons of data, you need to use iteration logic. As you can see in the above code, there are various ways to achieve iteration in Python. We can use iter, range, enumerate, and zip to concatenate two lists. In particular, the zip function may end when it faces the end of the item between the two lists.


## Transforms
```python
def filterFunc(x):
    if x % 2 == 0:
        return False 
    return True


def squareFunc(x):
    return x**2


def demo_transforms(): 
    nums = (1, 2, 3, 4, 5, 6)
    odds = list(filter(filterFunc, nums))
    print(odds) # [1, 3, 5]

    squares = list(map(squareFunc, nums))
    print(squares) # [1, 4, 9, 16, 25, 36]


demo_transforms()
```
Data transformation is one everyday task for those who handle data. If you want to filter out, you can find a [filter function document](https://docs.python.org/3/library/functions.html#filter). If you want to apply something to all elements in the list, then you have to look [map function document](https://docs.python.org/3/library/functions.html#map). 


## itertools
```python
def testFunction(x):
    return x < 40


def demo_itertools():
    seq1 = [1, 2, 3]
    # create an infinite cycle from the sequence
    cycle1 = itertools.cycle(seq1)
    print(next(cycle1)) # 1
    print(next(cycle1)) # 2
    print(next(cycle1)) # 3
    print(next(cycle1)) # 1
    print(next(cycle1)) # 1

    # count by increasing 10
    count1 = itertools.count(100, 10)
    print(next(count1)) # 100
    print(next(count1)) # 110
    print(next(count1)) # 120

    # accumulate the given operation
    vals = [10, 20, 30, 40, 50, 40, 30]
    acc = itertools.accumulate(vals, max) 
    print(list(acc)) # [10, 20, 30, 40, 50, 50, 50]

    # connect sequences together
    x = itertools.chain("ABCD", "1234")
    print(list(x)) # ['A', 'B', 'C', 'D', '1', '2', '3', '4']

    # drop a list of item until it meets False
    print(list(itertools.dropwhile(testFunction, vals))) 
    # [40, 50, 40, 30]
    # take a list of item until it meets False
    print(list(itertools.takewhile(testFunction, vals))) 
    # [10, 20, 30]


demo_itertools()
```
Here is the interesting [itertools document](https://docs.python.org/3/library/itertools.html) and in this post, I will introduce some of the functions from [a lecture](). **Cycle** function creates an infinite iterator. When we call next, it will print out an item in the sequence. If it faces the end of the sequence, it will back to the first item. **Count** function returns an iterator that counts by the given parameter. **Accumulate** applies a given operation to the list by increasing its index. **Chain** function concatenates the given sequences. **Dropwhile** and **Takewhile** might be a little tricky. **Dropwhile** function will drop when the predicate is "True" until it faces the first "False" value. **Takewhile** function is opposite for the dropwhile. 
