---
title: "Advanced Python - 2"
excerpt: "False values, Logical operation, String formatting in Python."
toc: true
toc_sticky: true 

categories:
    - Python
tags:
    - Python
last_modified_at: 2020-02-13T08:06:00-05:00
---

In this post, I've learned what could be evaluated as False values in Python, short-circuit operation in logical operation, String formatting in Python. 

## False value in Python 

* False and None evaluate to false 
* Numeric zero values: 0, 0.0, 0j
* Decimal(0), Fraction(0, x)
* Empty sequences/collections: '', (), [], {}
* Empty sets and ranges: set(), range(0)
* Custom object function overrides __bool__ return False or __len__ return 0 

These are the list of **false values in Python**. If we want to use conditional statements, this is what we should know about. It seems False values in Python are different from other languages.

```python
class Custom:
    def __len__(self):
        return 0

    def __bool__(self):
        return False


def print_false_value(): 
    print(False) # False
    print(bool(None)) # False
    print(bool('')) # False
    print(bool(range(0))) # False
    print(bool([])) # False
    print(bool({})) # False
    print(bool(Decimal(0))) # False
    c = Custom() 
    print(bool(c)) # False

print_false_value()
```

## Logical operation
* X and Y 
* X or Y 
* not X

The first two operations are called short-circuits operation. For 'and' operation, if X is False then Y will not be evaluated. For 'or' operation, when X is True then Y will not be evaluated. In the below code, the 'print and return false' won't be printed out because of the short-circuit operation. 

```python
def print_and_return_false():
    print('print and return false')
    return False


def check_short_circuit():
    print(True or print_and_return_false())
    print(False and print_and_return_false())

check_short_circuit()
```


## Strings vs bytes
```python
def binary_string():
    binary_str = b'ABCD'
    str1 = 'EFG'
    # print(binary_str + str1) # we can't cancatenate it directly
    print(binary_str + str1.encode())
    print(binary_str.decode() + str1)

binary_string()
```
Those are not concatenated directly. We need to handle this properly to concatenate it. I remembered that when I got a crawling task, I have to handle this properly.



## String formatting
<!-- 4 ways to template string -->
```python
from string import Template 

templ = Template("You're reading ${title} by ${author}")
str1 = templ.substitue(title="Dance with Programming", 
    author="Junhong Kim")
print(str1)

data = {
    'author': 'Junhong Kim',
    'title': 'Dance with Programming'
}
str2 = templ.substitue(data)
print(str2)

# f-string version from Python 3.6
title = 'Dance with Programming'
author = 'Junhong Kim'
str3 = f"You're reading {title} by {author}"
print(str3)
```
Instead of the format method in the str object in Python, this way is more obvious to print out. From Python 3.6, Python supports f-string. It's way more readable then any other way but if we want to use the f-string version, then we have to make sure the version of Python. 